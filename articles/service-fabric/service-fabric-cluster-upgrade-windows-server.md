---
title: "Обновление автономного кластера Azure Service Fabric в Windows Server | Документы Майкрософт"
description: "Обновление кода и (или) конфигурации Azure Service Fabric, под управлением которой работает автономный кластер Service Fabric, включая изменение режима обновления кластера."
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
ms.openlocfilehash: ac40775ca62362a32184207857a0b965a798e135
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="68d84-103">Обновление автономной службы Azure Service Fabric в кластере Windows Server</span><span class="sxs-lookup"><span data-stu-id="68d84-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68d84-104">Кластер Azure</span><span class="sxs-lookup"><span data-stu-id="68d84-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="68d84-105">Автономный кластер</span><span class="sxs-lookup"><span data-stu-id="68d84-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="68d84-106">Для любой современной системы возможность обновления является ключом к долговременному успеху вашего продукта.</span><span class="sxs-lookup"><span data-stu-id="68d84-106">For any modern system, the ability to upgrade is a key to the long-term success of your product.</span></span> <span data-ttu-id="68d84-107">Кластер Azure Service Fabric — это ресурс, владельцем которого вы являетесь.</span><span class="sxs-lookup"><span data-stu-id="68d84-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="68d84-108">В этой статье описывается, как настроить в кластере выполнение только поддерживаемых версий кода и конфигураций Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="68d84-108">This article describes how you can make sure that the cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-the-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="68d84-109">Управление версией Service Fabric в кластере</span><span class="sxs-lookup"><span data-stu-id="68d84-109">Control the Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="68d84-110">Чтобы настроить кластер для скачивания обновлений Service Fabric после того, как корпорация Майкрософт выпускает новую версию, присвойте параметру кластера **fabricClusterAutoupgradeEnabled** значение true.</span><span class="sxs-lookup"><span data-stu-id="68d84-110">To set your cluster to download updates of Service Fabric when Microsoft releases a new version, set the **fabricClusterAutoupgradeEnabled** cluster configuration to true.</span></span> <span data-ttu-id="68d84-111">Чтобы выбрать поддерживаемую версию Service Fabric для кластера, присвойте параметру кластера **fabricClusterAutoupgradeEnabled** значение false.</span><span class="sxs-lookup"><span data-stu-id="68d84-111">To select a supported version of Service Fabric that you want your cluster to be on, set the **fabricClusterAutoupgradeEnabled** cluster configuration to false.</span></span>

> [!NOTE]
> <span data-ttu-id="68d84-112">Кластер должен всегда работать под управлением поддерживаемой версии Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="68d84-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="68d84-113">Когда корпорация Майкрософт объявляет о выпуске новой версии Service Fabric, для предыдущей версии определяется срок завершения жизненного цикла. Этот срок составляет по меньшей мере 60 дней с даты объявления.</span><span class="sxs-lookup"><span data-stu-id="68d84-113">When Microsoft announces the release of a new version of Service Fabric, the previous version is marked for end of support after a minimum of 60 days from the date of the announcement.</span></span> <span data-ttu-id="68d84-114">О доступности новых выпусков сообщается в [блоге группы разработчиков Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric/),</span><span class="sxs-lookup"><span data-stu-id="68d84-114">New releases are announced [on the Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="68d84-115">после чего вы можете их использовать.</span><span class="sxs-lookup"><span data-stu-id="68d84-115">The new release is available to choose at that point.</span></span>
>
>

<span data-ttu-id="68d84-116">Кластер можно обновить до новой версии, только если используется конфигурация узла с настройками рабочей среды, где каждый узел Service Fabric выделяется для отдельного физического или виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="68d84-116">You can upgrade your cluster to the new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="68d84-117">Если несколько узлов Service Fabric выполняется на отдельном физическом компьютере или виртуальной машине в кластере разработки, то нужно удалить такой кластер и создать его заново с использованием новой версии.</span><span class="sxs-lookup"><span data-stu-id="68d84-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create the cluster with the new version.</span></span>

<span data-ttu-id="68d84-118">Обновить кластер до последней или поддерживаемой версии Service Fabric можно с помощью двух разных рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="68d84-118">Two distinct workflows can upgrade your cluster to the latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="68d84-119">Один используется для кластеров с возможностью подключения для автоматического скачивания последней версии.</span><span class="sxs-lookup"><span data-stu-id="68d84-119">One workflow is for clusters that have connectivity to download the latest version automatically.</span></span> <span data-ttu-id="68d84-120">Другой рабочий процесс используется для кластеров без возможности подключения для автоматического скачивания последней версии.</span><span class="sxs-lookup"><span data-stu-id="68d84-120">The other workflow is for clusters that do not have connectivity to download the latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="68d84-121">Обновление кластеров с возможностью подключения для скачивания последней версии кода и конфигурации</span><span class="sxs-lookup"><span data-stu-id="68d84-121">Upgrade clusters that have connectivity to download the latest code and configuration</span></span>
<span data-ttu-id="68d84-122">Выполните следующие действия, чтобы обновить кластер до поддерживаемой, если у него есть возможность подключения к сайту [http://download.microsoft.com](http://download.microsoft.com) через Интернет.</span><span class="sxs-lookup"><span data-stu-id="68d84-122">Use these steps to upgrade your cluster to a supported version if your cluster nodes have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="68d84-123">Для кластеров с возможностью подключения к [http://download.microsoft.com](http://download.microsoft.com) корпорация Майкрософт рекомендует периодически проверять наличие новых версий Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="68d84-123">For clusters that have connectivity to [http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for the availability of new Service Fabric versions.</span></span>

<span data-ttu-id="68d84-124">Когда выходит новая версия Service Fabric, пакет скачивается в кластер и начинается подготовка к обновлению.</span><span class="sxs-lookup"><span data-stu-id="68d84-124">When a new Service Fabric version is available, the package is downloaded locally to the cluster and provisioned for upgrade.</span></span> <span data-ttu-id="68d84-125">Наряду с информированием клиентов о доступности новой версии система выдает явное предупреждение о состоянии работоспособности кластера следующего содержания:</span><span class="sxs-lookup"><span data-stu-id="68d84-125">Additionally, to inform the customer of this new version, the system shows an explicit cluster health warning that's similar to the following:</span></span>

<span data-ttu-id="68d84-126">"Поддержка текущей версии кластера [номер версии] заканчивается [дата]".</span><span class="sxs-lookup"><span data-stu-id="68d84-126">“The current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="68d84-127">После запуска последней версии кластера это предупреждение исчезнет.</span><span class="sxs-lookup"><span data-stu-id="68d84-127">After the cluster is running the latest version, the warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="68d84-128">Рабочий процесс обновления кластера</span><span class="sxs-lookup"><span data-stu-id="68d84-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="68d84-129">Как только вы увидите предупреждение о работоспособности кластера, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="68d84-129">After you see the cluster health warning, do the following:</span></span>

1. <span data-ttu-id="68d84-130">Подключитесь к кластеру с любой виртуальной машины, на которой есть доступ администратора ко всем ВМ, перечисленным в качестве узлов в файле конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="68d84-130">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="68d84-131">Компьютер, на котором выполняется этот сценарий, может и не входить в кластер.</span><span class="sxs-lookup"><span data-stu-id="68d84-131">The machine that this script is run on does not have to be part of the cluster.</span></span>

    ```powershell

    ###### connect to the secure cluster using certs
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

2. <span data-ttu-id="68d84-132">Получите список версий Service Fabric, до которых можно выполнить обновление.</span><span class="sxs-lookup"><span data-stu-id="68d84-132">Get the list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="68d84-133">Должен отобразиться результат следующего вида.</span><span class="sxs-lookup"><span data-stu-id="68d84-133">You should get an output similar to this:</span></span>

    ![Получение версий Service Fabric][getfabversions]
3. <span data-ttu-id="68d84-135">Запустите обновление кластера до доступной версии с помощью команды PowerShell [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="68d84-135">Start a cluster upgrade to an available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="68d84-136">За ходом обновления можно следить в Service Fabric Explorer. Также можно выполнить следующую команду Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="68d84-136">To monitor the progress of the upgrade, you can use Service Fabric Explorer or run the following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="68d84-137">Если требования политик работоспособности кластера не реализуются, выполняется откат обновления.</span><span class="sxs-lookup"><span data-stu-id="68d84-137">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="68d84-138">О том, как указать пользовательские политики работоспособности для команды **Start-ServiceFabricClusterUpgrade**, можно узнать в [соответствующей документации](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="68d84-138">To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="68d84-139">Устранив проблемы, которые привели к откату, запустите обновление снова, выполнив уже описанные действия.</span><span class="sxs-lookup"><span data-stu-id="68d84-139">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="68d84-140">Обновление кластеров <U>без возможности подключения</u> для скачивания последней версии кода и конфигурации</span><span class="sxs-lookup"><span data-stu-id="68d84-140">Upgrade clusters that have <U>no connectivity</u> to download the latest code and configuration</span></span>
<span data-ttu-id="68d84-141">Выполните следующие действия, чтобы обновить до поддерживаемой версии кластер без возможности подключения к сайту [http://download.microsoft.com](http://download.microsoft.com) через Интернет.</span><span class="sxs-lookup"><span data-stu-id="68d84-141">Use these steps to upgrade your cluster to a supported version if your cluster nodes do not have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="68d84-142">Если вы используете кластер без подключения к Интернету, то потребуется отслеживать блог команды разработчиков Service Fabric, чтобы узнавать о новых выпусках.</span><span class="sxs-lookup"><span data-stu-id="68d84-142">If you are running a cluster that is not connected to the Internet, you will have to monitor the Service Fabric team blog to learn about a new release.</span></span> <span data-ttu-id="68d84-143">Система не будет показывать предупреждение о работоспособности кластера, чтобы оповещать вас о новом выпуске.</span><span class="sxs-lookup"><span data-stu-id="68d84-143">The system does not show a cluster health warning to alert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="68d84-144">Автоматическая подготовка и подготовка вручную</span><span class="sxs-lookup"><span data-stu-id="68d84-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="68d84-145">Чтобы включить автоматические операции скачивания и регистрации для получения последней версии кода, настройте службу обновления Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="68d84-145">To enable automatic downloading and registration for the latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="68d84-146">См. инструкции Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt, доступные в [изолированном пакете](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="68d84-146">Refer to the Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside the [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="68d84-147">Для выполнения операций вручную сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="68d84-147">For manual process, follow the instructions below.</span></span>

<span data-ttu-id="68d84-148">Прежде чем начать обновление конфигурации, измените конфигурацию кластера, присвоив следующему свойству значение false.</span><span class="sxs-lookup"><span data-stu-id="68d84-148">Modify your cluster configuration to set the following property to false before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="68d84-149">См. дополнительные сведения об использовании командлета [Start-ServiceFabricClusterConfigurationUpgrade](https://msdn.microsoft.com/en-us/library/mt788302.aspx).</span><span class="sxs-lookup"><span data-stu-id="68d84-149">Refer to [Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="68d84-150">Обязательно обновите параметр clusterConfigurationVersion в JSON, прежде чем запускать обновление конфигурации.</span><span class="sxs-lookup"><span data-stu-id="68d84-150">Make sure to update 'clusterConfigurationVersion' in your JSON before you start the configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="68d84-151">Рабочий процесс обновления кластера</span><span class="sxs-lookup"><span data-stu-id="68d84-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="68d84-152">Выполните командлет Get-ServiceFabricClusterUpgrade из одного из узлов в кластере и запишите значение TargetCodeVersion.</span><span class="sxs-lookup"><span data-stu-id="68d84-152">Run Get-ServiceFabricClusterUpgrade from one of the nodes in the cluster and note the TargetCodeVersion.</span></span>
2. <span data-ttu-id="68d84-153">Выполните следующую команду с компьютера, подключенного к Интернету, чтобы получить список всех версий, совместимых с обновлением, для текущей версии и скачайте соответствующий пакет с помощью связанных ссылок для загрузки.</span><span class="sxs-lookup"><span data-stu-id="68d84-153">Run the following from an internet connected machine to list all upgrade compatible versions with the current version and download the corresponding package from the associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="68d84-154">Подключитесь к кластеру с любой виртуальной машины, на которой есть доступ администратора ко всем ВМ, перечисленным в качестве узлов в файле конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="68d84-154">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="68d84-155">Виртуальная машина, на которой выполняется этот скрипт, может и не входить в кластер.</span><span class="sxs-lookup"><span data-stu-id="68d84-155">The machine that this script is run on does not have to be part of the cluster</span></span>

    ```powershell

   ###### Get the list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file including the path to it> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="68d84-156">Скопируйте скачанный пакет в хранилище образов кластера.</span><span class="sxs-lookup"><span data-stu-id="68d84-156">Copy the downloaded package into the cluster image store.</span></span>

5. <span data-ttu-id="68d84-157">Зарегистрируйте скопированный пакет.</span><span class="sxs-lookup"><span data-stu-id="68d84-157">Register the copied package.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="68d84-158">Запустите обновление кластера до доступной версии.</span><span class="sxs-lookup"><span data-stu-id="68d84-158">Start a cluster upgrade to an available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="68d84-159">За ходом обновления можно следить в Service Fabric Explorer. Можно также выполнить следующую команду PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68d84-159">You can monitor the progress of the upgrade on Service Fabric Explorer, or you can run the following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="68d84-160">Если требования политик работоспособности кластера не реализуются, выполняется откат обновления.</span><span class="sxs-lookup"><span data-stu-id="68d84-160">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="68d84-161">О том, как указать пользовательские политики работоспособности для команды **Start-ServiceFabricClusterUpgrade**, можно узнать в [соответствующей документации](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="68d84-161">To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see the documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="68d84-162">Устранив проблемы, которые привели к откату, запустите обновление снова, выполнив уже описанные действия.</span><span class="sxs-lookup"><span data-stu-id="68d84-162">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>


## <a name="upgrade-the-cluster-configuration"></a><span data-ttu-id="68d84-163">Обновление конфигурации кластера</span><span class="sxs-lookup"><span data-stu-id="68d84-163">Upgrade the cluster configuration</span></span>
<span data-ttu-id="68d84-164">Прежде чем начинать обновление конфигурации, можно протестировать новый JSON-файл конфигурации кластера, выполнив сценарий Powershell в изолированном пакете.</span><span class="sxs-lookup"><span data-stu-id="68d84-164">Before you initiate the configuration upgrade, you can test your new cluster configuration json by running the powershell script in the standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File>

```
<span data-ttu-id="68d84-165">или</span><span class="sxs-lookup"><span data-stu-id="68d84-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File> -FabricRuntimePackagePath <Path to the .cab file which you want to test the configuration against>

```

<span data-ttu-id="68d84-166">Некоторые конфигурации невозможно обновить, например конечные точки, имена кластеров, IP-адреса узлов и т. д. Таким образом мы протестируем новый JSON-файл конфигурации кластера, используя старый файл. При наличии каких-либо проблем в окне Powershell отобразятся сведения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="68d84-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test the new cluster configuration json against the old one and throw errors in the Powershell window if there is any issue.</span></span>

<span data-ttu-id="68d84-167">Чтобы обновить конфигурацию кластера, выполните команду **Start-ServiceFabricClusterConfigurationUpgrade**.</span><span class="sxs-lookup"><span data-stu-id="68d84-167">To upgrade the cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="68d84-168">Обновление конфигурации обрабатывает домен обновления.</span><span class="sxs-lookup"><span data-stu-id="68d84-168">The configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="68d84-169">Обновление конфигурации сертификата кластера</span><span class="sxs-lookup"><span data-stu-id="68d84-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="68d84-170">Сертификат кластера используется для аутентификации между узлами кластера, поэтому смену сертификата следует выполнять с особой осторожностью, так как из-за сбоя заблокируется связь между узлами кластера.</span><span class="sxs-lookup"><span data-stu-id="68d84-170">Cluster certificate is used for authentication between cluster nodes, so the certificate roll over should be performed with extra caution because failure will block the communication among cluster nodes.</span></span>  
<span data-ttu-id="68d84-171">Технически поддерживаются три варианта:</span><span class="sxs-lookup"><span data-stu-id="68d84-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="68d84-172">Единое обновление сертификата. Путь обновления: ''сертификат А (основной) -> сертификат B (основной) -> сертификат C (основной) ->...''.</span><span class="sxs-lookup"><span data-stu-id="68d84-172">Single certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="68d84-173">Двойное обновление сертификата. Путь обновления ''сертификат А (основной) -> сертификат А (основной) и В (дополнительный) -> сертификат В (основной) -> сертификат В (основной) и С (дополнительный) -> сертификат C (основной)->…''.</span><span class="sxs-lookup"><span data-stu-id="68d84-173">Double certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="68d84-174">Тип обновления сертификатов: сертификат на основе отпечатка <-> сертификаты на основе конфигурации CommonName.</span><span class="sxs-lookup"><span data-stu-id="68d84-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="68d84-175">Например, отпечаток сертификата A (основной) и отпечаток B (дополнительный) -> CommonName сертификата C.</span><span class="sxs-lookup"><span data-stu-id="68d84-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="68d84-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68d84-176">Next steps</span></span>
* <span data-ttu-id="68d84-177">Узнайте, как настроить некоторые [параметры кластера Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="68d84-177">Learn how to customize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="68d84-178">Ознакомьтесь с концепцией [масштабирования кластера](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="68d84-178">Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="68d84-179">Узнайте об [обновлениях приложений](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="68d84-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
