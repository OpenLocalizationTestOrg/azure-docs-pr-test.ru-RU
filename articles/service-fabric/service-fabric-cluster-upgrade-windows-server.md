---
title: "aaaUpgrade автономного Azure Service Fabric кластера в Windows Server | Документы Microsoft"
description: "Обновление Azure Service Fabric кода hello и/или конфигурацию, которая запускает кластера Service Fabric автономный, включая настройку hello режим обновления кластера."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="a078a-103">Обновление автономной службы Azure Service Fabric в кластере Windows Server</span><span class="sxs-lookup"><span data-stu-id="a078a-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a078a-104">Кластер Azure</span><span class="sxs-lookup"><span data-stu-id="a078a-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="a078a-105">Автономный кластер</span><span class="sxs-lookup"><span data-stu-id="a078a-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="a078a-106">Для любой современной системе возможность tooupgrade hello — долгосрочный успех toohello ключа продукта.</span><span class="sxs-lookup"><span data-stu-id="a078a-106">For any modern system, hello ability tooupgrade is a key toohello long-term success of your product.</span></span> <span data-ttu-id="a078a-107">Кластер Azure Service Fabric — это ресурс, владельцем которого вы являетесь.</span><span class="sxs-lookup"><span data-stu-id="a078a-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="a078a-108">Этой статье описывается, как сделать убедиться, что данный кластер hello всегда выполняется поддерживаемые версии кода структуры службы и конфигураций.</span><span class="sxs-lookup"><span data-stu-id="a078a-108">This article describes how you can make sure that hello cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="a078a-109">Элемент управления hello Service Fabric версии, работающей в кластере</span><span class="sxs-lookup"><span data-stu-id="a078a-109">Control hello Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="a078a-110">tooset Service Fabric, когда корпорация Майкрософт выпускает новую версию набора hello обновляет вашего кластера toodownload **fabricClusterAutoupgradeEnabled** tootrue конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="a078a-110">tooset your cluster toodownload updates of Service Fabric when Microsoft releases a new version, set hello **fabricClusterAutoupgradeEnabled** cluster configuration tootrue.</span></span> <span data-ttu-id="a078a-111">поддерживаемая версия Service Fabric, которые должны toobe вашего кластера на набор hello tooselect **fabricClusterAutoupgradeEnabled** toofalse конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="a078a-111">tooselect a supported version of Service Fabric that you want your cluster toobe on, set hello **fabricClusterAutoupgradeEnabled** cluster configuration toofalse.</span></span>

> [!NOTE]
> <span data-ttu-id="a078a-112">Кластер должен всегда работать под управлением поддерживаемой версии Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a078a-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="a078a-113">Когда корпорация Майкрософт объявляет о выпуске новой версии Service Fabric hello, предыдущей версии hello помечена для окончания поддержки после менее 60 дней с даты hello объявления «hello».</span><span class="sxs-lookup"><span data-stu-id="a078a-113">When Microsoft announces hello release of a new version of Service Fabric, hello previous version is marked for end of support after a minimum of 60 days from hello date of hello announcement.</span></span> <span data-ttu-id="a078a-114">Новые выпуски, объявляются [в блоге группы Service Fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="a078a-114">New releases are announced [on hello Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="a078a-115">Новый выпуск Hello — доступные toochoose на данный момент.</span><span class="sxs-lookup"><span data-stu-id="a078a-115">hello new release is available toochoose at that point.</span></span>
>
>

<span data-ttu-id="a078a-116">Новая версия toohello кластера можно обновить только в том случае, если вы используете стиль рабочей конфигурации узла, где каждый узел Service Fabric выделяется на отдельной физической или виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a078a-116">You can upgrade your cluster toohello new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="a078a-117">При наличии кластеру разработки, где более чем одним узлом Service Fabric — на отдельной физической или виртуальной машине, необходимо повторно создать кластер hello hello новой версии.</span><span class="sxs-lookup"><span data-stu-id="a078a-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create hello cluster with hello new version.</span></span>

<span data-ttu-id="a078a-118">Последнюю версию toohello кластера или поддерживаемая версия Service Fabric, можно обновить два различных рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="a078a-118">Two distinct workflows can upgrade your cluster toohello latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="a078a-119">Кластеры с подключением toodownload hello последнюю версию автоматически — одного рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="a078a-119">One workflow is for clusters that have connectivity toodownload hello latest version automatically.</span></span> <span data-ttu-id="a078a-120">Hello другой рабочий процесс — для кластеров, у которых нет подключения к toodownload hello последнюю версию, Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a078a-120">hello other workflow is for clusters that do not have connectivity toodownload hello latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="a078a-121">Обновление кластеров, которые имеют подключения toodownload hello последнюю кода и конфигурации</span><span class="sxs-lookup"><span data-stu-id="a078a-121">Upgrade clusters that have connectivity toodownload hello latest code and configuration</span></span>
<span data-ttu-id="a078a-122">Использовать эти действия tooupgrade версии tooa поддерживается кластера, если узлы кластера подключен к Интернету слишком[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a078a-122">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="a078a-123">Кластеры с подключением слишком[http://download.microsoft.com](http://download.microsoft.com), корпорация Майкрософт периодически проверяет доступность hello новые версии Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a078a-123">For clusters that have connectivity too[http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for hello availability of new Service Fabric versions.</span></span>

<span data-ttu-id="a078a-124">Если доступна новая версия Service Fabric, hello пакет будет загружен локально toohello кластера и Подготовка к обновлению.</span><span class="sxs-lookup"><span data-stu-id="a078a-124">When a new Service Fabric version is available, hello package is downloaded locally toohello cluster and provisioned for upgrade.</span></span> <span data-ttu-id="a078a-125">Кроме того клиент hello tooinform этой новой версии, hello система выводит предупреждение работоспособности явную кластера, аналогичные toohello следующие:</span><span class="sxs-lookup"><span data-stu-id="a078a-125">Additionally, tooinform hello customer of this new version, hello system shows an explicit cluster health warning that's similar toohello following:</span></span>

<span data-ttu-id="a078a-126">«hello поддержка кластера версии [номер версии] заканчивается на [дата].»</span><span class="sxs-lookup"><span data-stu-id="a078a-126">“hello current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="a078a-127">После запуска кластера hello последнюю версию hello hello предупреждение исчезнет.</span><span class="sxs-lookup"><span data-stu-id="a078a-127">After hello cluster is running hello latest version, hello warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="a078a-128">Рабочий процесс обновления кластера</span><span class="sxs-lookup"><span data-stu-id="a078a-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="a078a-129">После появления предупреждения работоспособности кластера hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a078a-129">After you see hello cluster health warning, do hello following:</span></span>

1. <span data-ttu-id="a078a-130">Подключите кластер toohello с любого компьютера, которая содержит компьютеры hello tooall доступа администратора, указываются в виде узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-130">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="a078a-131">машина Hello, этот сценарий выполняется на имеет toobe частью кластера hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-131">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. <span data-ttu-id="a078a-132">Получите список hello Service Fabric версий, которые можно обновить до.</span><span class="sxs-lookup"><span data-stu-id="a078a-132">Get hello list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="a078a-133">Вы должны получить аналогичные toothis выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a078a-133">You should get an output similar toothis:</span></span>

    ![Получение версий Service Fabric][getfabversions]
3. <span data-ttu-id="a078a-135">Запуска версии доступны обновления tooan кластера с помощью [ServiceFabricClusterUpgrade начала](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span><span class="sxs-lookup"><span data-stu-id="a078a-135">Start a cluster upgrade tooan available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="a078a-136">toomonitor hello ход выполнения обновления hello, можно использовать обозреватель Service Fabric или выполнения hello следующую команду Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a078a-136">toomonitor hello progress of hello upgrade, you can use Service Fabric Explorer or run hello following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="a078a-137">Если политики работоспособности кластера hello не выполняются, выполняется откат обновления hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-137">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="a078a-138">toospecify работоспособности пользовательских политик для hello **начала ServiceFabricClusterUpgrade** см. в разделе документации по [ServiceFabricClusterUpgrade начала](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="a078a-138">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="a078a-139">После устранения проблемы hello, приводящие к отката hello инициировать попытку обновления hello, следующие hello же действия как описано выше.</span><span class="sxs-lookup"><span data-stu-id="a078a-139">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="a078a-140">Обновление кластеров, которые имеют <U>без подключения к</u> toodownload hello последнюю кода и конфигурации</span><span class="sxs-lookup"><span data-stu-id="a078a-140">Upgrade clusters that have <U>no connectivity</u> toodownload hello latest code and configuration</span></span>
<span data-ttu-id="a078a-141">Использовать эти действия tooupgrade версии tooa поддерживается кластера, если узлы кластера не подключен к Интернету слишком[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a078a-141">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes do not have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="a078a-142">При запуске кластера, не подключенной toohello Интернет имеется toolearn toomonitor hello Service Fabric team блог о новом выпуске.</span><span class="sxs-lookup"><span data-stu-id="a078a-142">If you are running a cluster that is not connected toohello Internet, you will have toomonitor hello Service Fabric team blog toolearn about a new release.</span></span> <span data-ttu-id="a078a-143">система Hello не содержит tooalert предупреждение работоспособности кластера вы нового выпуска.</span><span class="sxs-lookup"><span data-stu-id="a078a-143">hello system does not show a cluster health warning tooalert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="a078a-144">Автоматическая подготовка и подготовка вручную</span><span class="sxs-lookup"><span data-stu-id="a078a-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="a078a-145">Автоматическая загрузка tooenable и регистрацию для последней версии кода hello, настройте служба Service Fabric обновления.</span><span class="sxs-lookup"><span data-stu-id="a078a-145">tooenable automatic downloading and registration for hello latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="a078a-146">См. toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt внутри hello [изолированный пакет](service-fabric-cluster-standalone-package-contents.md) инструкции.</span><span class="sxs-lookup"><span data-stu-id="a078a-146">Refer toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside hello [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="a078a-147">Для ручной процесс следуйте приведенным ниже инструкциям hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-147">For manual process, follow hello instructions below.</span></span>

<span data-ttu-id="a078a-148">Измените следующие свойства toofalse, прежде чем начать обновление конфигурации вашей tooset hello кластера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a078a-148">Modify your cluster configuration tooset hello following property toofalse before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="a078a-149">См. слишком[ServiceFabricClusterConfigurationUpgrade начала PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) сведения об использовании.</span><span class="sxs-lookup"><span data-stu-id="a078a-149">Refer too[Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="a078a-150">Убедитесь, что tooupdate «clusterConfigurationVersion» в JSON перед началом обновления конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-150">Make sure tooupdate 'clusterConfigurationVersion' in your JSON before you start hello configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="a078a-151">Рабочий процесс обновления кластера</span><span class="sxs-lookup"><span data-stu-id="a078a-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="a078a-152">Запустите Get-ServiceFabricClusterUpgrade в одном из узлов hello в кластере hello и отметьте hello TargetCodeVersion.</span><span class="sxs-lookup"><span data-stu-id="a078a-152">Run Get-ServiceFabricClusterUpgrade from one of hello nodes in hello cluster and note hello TargetCodeVersion.</span></span>
2. <span data-ttu-id="a078a-153">Выполнения hello следующие данные из подключенного машина internet toolist все обновления совместимые версии с текущей версией hello и загрузите соответствующий пакет из ссылки для загрузки связанного hello hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-153">Run hello following from an internet connected machine toolist all upgrade compatible versions with hello current version and download hello corresponding package from hello associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="a078a-154">Подключите кластер toohello с любого компьютера, которая содержит компьютеры hello tooall доступа администратора, указываются в виде узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-154">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="a078a-155">Нет машины Hello, этот сценарий выполняется на toobe частью кластера hello</span><span class="sxs-lookup"><span data-stu-id="a078a-155">hello machine that this script is run on does not have toobe part of hello cluster</span></span>

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="a078a-156">Скопируйте пакет hello загружаются в хранилище образов кластера hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-156">Copy hello downloaded package into hello cluster image store.</span></span>

5. <span data-ttu-id="a078a-157">Регистрация пакета копируются hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-157">Register hello copied package.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="a078a-158">Запуска версии доступны обновления tooan кластера.</span><span class="sxs-lookup"><span data-stu-id="a078a-158">Start a cluster upgrade tooan available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="a078a-159">Можно отслеживать ход выполнения обновления hello на Service Fabric Explorer hello, или можно выполнить следующую команду PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-159">You can monitor hello progress of hello upgrade on Service Fabric Explorer, or you can run hello following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="a078a-160">Если политики работоспособности кластера hello не выполняются, выполняется откат обновления hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-160">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="a078a-161">toospecify работоспособности пользовательских политик для hello **начала ServiceFabricClusterUpgrade** см. в разделе документации hello [ServiceFabricClusterUpgrade начала](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="a078a-161">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see hello documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="a078a-162">После устранения проблемы hello, приводящие к отката hello инициировать попытку обновления hello, следующие hello же действия как описано выше.</span><span class="sxs-lookup"><span data-stu-id="a078a-162">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>


## <a name="upgrade-hello-cluster-configuration"></a><span data-ttu-id="a078a-163">Обновление конфигурации кластера hello</span><span class="sxs-lookup"><span data-stu-id="a078a-163">Upgrade hello cluster configuration</span></span>
<span data-ttu-id="a078a-164">Прежде чем начать обновление конфигурации hello, путем выполнения сценария powershell hello в hello изолированный пакет можно проверить новый json конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="a078a-164">Before you initiate hello configuration upgrade, you can test your new cluster configuration json by running hello powershell script in hello standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
<span data-ttu-id="a078a-165">или</span><span class="sxs-lookup"><span data-stu-id="a078a-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

<span data-ttu-id="a078a-166">Некоторые конфигурации невозможно обновить, например конечные точки, имена кластеров, IP-адреса узлов и т. д. Это тестирования hello нового кластера конфигурации json для старого hello и приводят к ошибкам в окне Powershell hello при наличии любые проблемы.</span><span class="sxs-lookup"><span data-stu-id="a078a-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test hello new cluster configuration json against hello old one and throw errors in hello Powershell window if there is any issue.</span></span>

<span data-ttu-id="a078a-167">Обновление конфигурации кластера tooupgrade hello, запустите **ServiceFabricClusterConfigurationUpgrade начала**.</span><span class="sxs-lookup"><span data-stu-id="a078a-167">tooupgrade hello cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="a078a-168">Обработанные домен обновления, домен обновления — обновление конфигурации Hello.</span><span class="sxs-lookup"><span data-stu-id="a078a-168">hello configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="a078a-169">Обновление конфигурации сертификата кластера</span><span class="sxs-lookup"><span data-stu-id="a078a-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="a078a-170">Кластер сертификат используется для проверки подлинности между узлами кластера, поэтому перезапись сертификатов hello следует выполнять в внимательно из-за сбоя заблокирует hello связи между узлами кластера.</span><span class="sxs-lookup"><span data-stu-id="a078a-170">Cluster certificate is used for authentication between cluster nodes, so hello certificate roll over should be performed with extra caution because failure will block hello communication among cluster nodes.</span></span>  
<span data-ttu-id="a078a-171">Технически поддерживаются три варианта:</span><span class="sxs-lookup"><span data-stu-id="a078a-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="a078a-172">Обновление одного сертификата: hello вариант предусматривает обновление "сертификат (основной) -> B сертификата (основной) -> C сертификата (основной) ->...".</span><span class="sxs-lookup"><span data-stu-id="a078a-172">Single certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="a078a-173">Double обновление сертификата: hello вариант предусматривает обновление "-> (основной) сертификата сертификата (основной) и B (дополнительный) -> B сертификата (основной) -> B сертификата (основной) и C (дополнительный) -> C сертификата (основной) ->...".</span><span class="sxs-lookup"><span data-stu-id="a078a-173">Double certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="a078a-174">Тип обновления сертификатов: сертификат на основе отпечатка <-> сертификаты на основе конфигурации CommonName.</span><span class="sxs-lookup"><span data-stu-id="a078a-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="a078a-175">Например, отпечаток сертификата A (основной) и отпечаток B (дополнительный) -> CommonName сертификата C.</span><span class="sxs-lookup"><span data-stu-id="a078a-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a078a-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a078a-176">Next steps</span></span>
* <span data-ttu-id="a078a-177">Узнайте, как toocustomize некоторые [параметры кластера Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="a078a-177">Learn how toocustomize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="a078a-178">Узнайте, каким образом слишком[масштабирования кластера](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="a078a-178">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="a078a-179">Узнайте об [обновлениях приложений](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="a078a-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
