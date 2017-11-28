---
title: "aaaCreate кластера Azure Service Fabric автономный | Документы Microsoft"
description: "Создание кластера Azure Service Fabric на любом компьютере (физическом сервере или виртуальной машине) под управлением Windows Server, расположенном в локальной системе или любом облаке."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="aaab3-103">Создание изолированного кластера под управлением Windows Server</span><span class="sxs-lookup"><span data-stu-id="aaab3-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="aaab3-104">Azure Service Fabric toocreate структуры службы кластеров можно использовать на любой виртуальной машины или компьютеры под управлением Windows Server.</span><span class="sxs-lookup"><span data-stu-id="aaab3-104">You can use Azure Service Fabric toocreate Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="aaab3-105">Это означает, что вы сможете разворачивать и запускать приложения Service Fabric в любой среде с набором подключенных друг к другу компьютеров с Windows Server как в локальной среде, так и у любого поставщика облачных служб.</span><span class="sxs-lookup"><span data-stu-id="aaab3-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="aaab3-106">Предоставляет Service Fabric toocreate пакета установки, кластеров Service Fabric вызывается hello изолированный пакет Windows Server.</span><span class="sxs-lookup"><span data-stu-id="aaab3-106">Service Fabric provides a setup package toocreate Service Fabric clusters called hello standalone Windows Server package.</span></span>

<span data-ttu-id="aaab3-107">В этой статье содержится описание этапов hello для создания автономного кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="aaab3-107">This article walks you through hello steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="aaab3-108">Этот изолированный пакет Windows Server сейчас доступен на коммерческой основе и может использоваться для рабочих развертываний.</span><span class="sxs-lookup"><span data-stu-id="aaab3-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="aaab3-109">Этот пакет может содержать новые функции Service Fabric, которые находятся на этапе предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="aaab3-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="aaab3-110">Прокрутите вниз слишком»[Предварительный просмотр компонентов, включенных в этот пакет](#previewfeatures_anchor).»</span><span class="sxs-lookup"><span data-stu-id="aaab3-110">Scroll down too"[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="aaab3-111">раздел для списка hello hello функции предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="aaab3-111">section for hello list of hello preview features.</span></span> <span data-ttu-id="aaab3-112">Вы можете [загрузить копию hello лицензионное соглашение](http://go.microsoft.com/fwlink/?LinkID=733084) сейчас.</span><span class="sxs-lookup"><span data-stu-id="aaab3-112">You can [download a copy of hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="aaab3-113">Получение поддержки для hello пакет Service Fabric для Windows Server</span><span class="sxs-lookup"><span data-stu-id="aaab3-113">Get support for hello Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="aaab3-114">Попросите hello сообщества о изолированный пакет Service Fabric hello для Windows Server hello [форум Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="aaab3-114">Ask hello community about hello Service Fabric standalone package for Windows Server in hello [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="aaab3-115">Откройте запрос на [техническую поддержку для Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="aaab3-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="aaab3-116">Узнайте больше о [профессиональной технической поддержке Майкрософт](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="aaab3-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="aaab3-117">Поддержка для этого пакета также доступна в рамках [поддержки Microsoft Premier](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="aaab3-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="aaab3-118">Дополнительные сведения см. в разделе [Варианты поддержки Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="aaab3-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="aaab3-119">toocollect журналы в целях поддержки запуска hello [сборщик журналов автономной службы структуры](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="aaab3-119">toocollect logs for support purposes, run hello [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="aaab3-120">Загрузить пакет Service Fabric для Windows Server hello</span><span class="sxs-lookup"><span data-stu-id="aaab3-120">Download hello Service Fabric for Windows Server package</span></span>
<span data-ttu-id="aaab3-121">кластер toocreate hello, используйте пакет Service Fabric для Windows Server hello (Windows Server 2012 R2 и более поздних) по следующему адресу:</span><span class="sxs-lookup"><span data-stu-id="aaab3-121">toocreate hello cluster, use hello Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="aaab3-122">
[Ссылка для скачивания изолированного пакета Service Fabric для Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="aaab3-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="aaab3-123">Найти подробные сведения о содержимом пакета hello [здесь](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="aaab3-123">Find details on contents of hello package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="aaab3-124">пакет среды выполнения Service Fabric Hello автоматически загружаются во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="aaab3-124">hello Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="aaab3-125">Если развертывание с компьютера не подключен toohello Интернет, загрузите пакет среды выполнения hello аппаратного здесь:</span><span class="sxs-lookup"><span data-stu-id="aaab3-125">If deploying from a machine not connected toohello internet, please download hello runtime package out of band from here:</span></span> <br><span data-ttu-id="aaab3-126">
[Ссылка для скачивания среды выполнения Service Fabric для Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="aaab3-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="aaab3-127">Примеры конфигурации изолированного кластера доступны здесь:</span><span class="sxs-lookup"><span data-stu-id="aaab3-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="aaab3-128">
[Примеры конфигурации изолированного кластера](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="aaab3-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a><span data-ttu-id="aaab3-129">Создание кластера hello</span><span class="sxs-lookup"><span data-stu-id="aaab3-129">Create hello cluster</span></span>
<span data-ttu-id="aaab3-130">Service Fabric может быть развернутой tooa кластеру разработки один компьютер с помощью hello *ClusterConfig.Unsecure.DevCluster.json* файл, включенный в [образцы](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="aaab3-130">Service Fabric can be deployed tooa one-machine development cluster by using hello *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="aaab3-131">Распакуйте пакет tooyour hello автономную машину, копировать hello образец конфигурации файла toohello локального компьютера, а затем выполнения hello *CreateServiceFabricCluster.ps1* скрипта через сеанс администратора PowerShell из автономной системы hello папка пакета:</span><span class="sxs-lookup"><span data-stu-id="aaab3-131">Unpack hello standalone package tooyour machine, copy hello sample config file toohello local machine, then run hello *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from hello standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="aaab3-132">Шаг 1А. Создание незащищенного локального кластера разработки</span><span class="sxs-lookup"><span data-stu-id="aaab3-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="aaab3-133">. В разделе hello раздел установки среды [планирование и Подготовка развертывания кластера](service-fabric-cluster-standalone-deployment-preparation.md) для устранения неполадок сведения.</span><span class="sxs-lookup"><span data-stu-id="aaab3-133">See hello Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="aaab3-134">Если завершения выполнения сценариев разработки можно удалить кластер Service Fabric hello hello машины с помощью ссылки toosteps в разделе «[удаления кластера](#removecluster_anchor)».</span><span class="sxs-lookup"><span data-stu-id="aaab3-134">If you're finished running development scenarios, you can remove hello Service Fabric cluster from hello machine by referring toosteps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="aaab3-135">Шаг 1Б. Создание кластера с несколькими компьютерами</span><span class="sxs-lookup"><span data-stu-id="aaab3-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="aaab3-136">После планирования hello проверены и действия по подготовке подробно описаны на странице приветствия приведенную ниже ссылку, вы готовы toocreate производственного кластера с использованием файла конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="aaab3-136">After you have gone through hello planning and preparation steps detailed at hello below link, you are ready toocreate your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="aaab3-137">
[Планирование и подготовка развертывания кластера](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="aaab3-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="aaab3-138">Проверить файл конфигурации hello написания, запустив hello *TestConfiguration.ps1* скрипта из папки пакета автономный hello:</span><span class="sxs-lookup"><span data-stu-id="aaab3-138">Validate hello configuration file you have written by running hello *TestConfiguration.ps1* script from hello standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="aaab3-139">Вы должны увидеть результат следующего вида.</span><span class="sxs-lookup"><span data-stu-id="aaab3-139">You should see output like below.</span></span> <span data-ttu-id="aaab3-140">Если hello нижнего поля «Выполнено» возвращается как «True», проверок работоспособности и кластера hello выглядит toobe развертываемых на основе конфигурации ввода hello.</span><span class="sxs-lookup"><span data-stu-id="aaab3-140">If hello bottom field "Passed" is returned as "True", sanity checks have passed and hello cluster looks toobe deployable based on hello input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. <span data-ttu-id="aaab3-141">Создание кластера hello: запустите hello *CreateServiceFabricCluster.ps1* кластера Service Fabric hello toodeploy скрипт на каждой машине в конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="aaab3-141">Create hello cluster:  Run hello *CreateServiceFabricCluster.ps1* script toodeploy hello Service Fabric cluster across each machine in hello configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="aaab3-142">Развертывание трассировки записываются toohello ВМ/machine запуска сценария CreateServiceFabricCluster.ps1 PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="aaab3-142">Deployment traces are written toohello VM/machine on which you ran hello CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="aaab3-143">Они находятся во вложенной папке hello DeploymentTraces, на основе в каталоге hello, из которого hello запуска сценария.</span><span class="sxs-lookup"><span data-stu-id="aaab3-143">These can be found in hello subfolder DeploymentTraces, based in hello directory from which hello script was run.</span></span> <span data-ttu-id="aaab3-144">toosee Если Service Fabric был развернут правильно tooa машины, найти hello установлены файлы в каталоге FabricDataRoot hello, как описано в файле конфигурации кластера hello раздел FabricSettings (по умолчанию c:\ProgramData\SF).</span><span class="sxs-lookup"><span data-stu-id="aaab3-144">toosee if Service Fabric was deployed correctly tooa machine, find hello installed files in hello FabricDataRoot directory, as detailed in hello cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="aaab3-145">Кроме того, процессы FabricHost.exe и Fabric.exe должны отображаться в диспетчере задач.</span><span class="sxs-lookup"><span data-stu-id="aaab3-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="aaab3-146">Шаг 1в. Создание кластера в автономном состоянии (не подключенного к Интернету)</span><span class="sxs-lookup"><span data-stu-id="aaab3-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="aaab3-147">пакет среды выполнения Service Fabric Hello автоматически загружаются при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="aaab3-147">hello Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="aaab3-148">При развертывании toomachines кластера не подключения toohello Интернета, необходимо будет toodownload hello Service Fabric среды выполнения пакета отдельно и предоставить tooit путь hello в момент создания кластера.</span><span class="sxs-lookup"><span data-stu-id="aaab3-148">When deploying a cluster toomachines not connected toohello internet, you will need toodownload hello Service Fabric runtime package separately, and provide hello path tooit at cluster creation.</span></span>
<span data-ttu-id="aaab3-149">Hello пакета среды выполнения может быть загружен отдельно, с другого компьютера подключен toohello Интернета, в [ссылку Загрузить - среда выполнения Service Fabric - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="aaab3-149">hello runtime package can be downloaded separately, from another machine connected toohello internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="aaab3-150">Скопируйте hello среды выполнения пакета toowhere вы развертываете hello вне сети кластера из и создание кластера hello, запустив `CreateServiceFabricCluster.ps1` с hello `-FabricRuntimePackagePath` параметр включен, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="aaab3-150">Copy hello runtime package toowhere you are deploying hello offline cluster from, and create hello cluster by running `CreateServiceFabricCluster.ps1` with hello `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="aaab3-151">где `.\ClusterConfig.json` и `.\MicrosoftAzureServiceFabric.cab` соответственно, конфигурация кластера toohello пути hello и hello среды выполнения CAB-файл.</span><span class="sxs-lookup"><span data-stu-id="aaab3-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are hello paths toohello cluster configuration and hello runtime .cab file respectively.</span></span>


### <a name="step-2-connect-toohello-cluster"></a><span data-ttu-id="aaab3-152">Шаг 2: Подключение toohello кластера</span><span class="sxs-lookup"><span data-stu-id="aaab3-152">Step 2: Connect toohello cluster</span></span>
<span data-ttu-id="aaab3-153">tooconnect tooa безопасного кластера, в разделе [Service fabric подключения кластера toosecure](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="aaab3-153">tooconnect tooa secure cluster, see [Service fabric connect toosecure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="aaab3-154">небезопасные кластер tooan tooconnect, запустите следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="aaab3-154">tooconnect tooan unsecure cluster, run hello following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="aaab3-155">Пример:</span><span class="sxs-lookup"><span data-stu-id="aaab3-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="aaab3-156">Шаг 3. Вызов Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="aaab3-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="aaab3-157">Теперь можно подключиться, используя обозреватель Service Fabric либо непосредственно из одной из машин hello http://localhost:19080/Explorer/index.html или удаленно с http://< toohello кластера*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.</span><span class="sxs-lookup"><span data-stu-id="aaab3-157">Now you can connect toohello cluster with Service Fabric Explorer either directly from one of hello machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="aaab3-158">Добавление и удаление узлов</span><span class="sxs-lookup"><span data-stu-id="aaab3-158">Add and remove nodes</span></span>
<span data-ttu-id="aaab3-159">Можно добавить или удалить кластер Service Fabric автономные узлы tooyour при изменении потребностей вашего бизнеса.</span><span class="sxs-lookup"><span data-stu-id="aaab3-159">You can add or remove nodes tooyour standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="aaab3-160">В разделе [добавления или удаления узлов tooa Service Fabric автономный кластера](service-fabric-cluster-windows-server-add-remove-nodes.md) подробное описание шагов.</span><span class="sxs-lookup"><span data-stu-id="aaab3-160">See [Add or Remove nodes tooa Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="aaab3-161">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="aaab3-161">Remove a cluster</span></span>
<span data-ttu-id="aaab3-162">tooremove кластера, запустите hello *RemoveServiceFabricCluster.ps1* сценарий PowerShell из папки пакета hello и передайте его в файл конфигурации JSON toohello путь hello.</span><span class="sxs-lookup"><span data-stu-id="aaab3-162">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="aaab3-163">При необходимости можно указать расположение для журнала hello hello операции удаления.</span><span class="sxs-lookup"><span data-stu-id="aaab3-163">You can optionally specify a location for hello log of hello deletion.</span></span>

<span data-ttu-id="aaab3-164">Этот сценарий может выполняться на любом компьютере с установленными машины hello tooall доступа администратора, перечисленных в файле конфигурации кластера hello как узлы.</span><span class="sxs-lookup"><span data-stu-id="aaab3-164">This script can be run on any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster configuration file.</span></span> <span data-ttu-id="aaab3-165">машина Hello, этот сценарий выполняется на имеет toobe частью кластера hello.</span><span class="sxs-lookup"><span data-stu-id="aaab3-165">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a><span data-ttu-id="aaab3-166">Собираемые данные телеметрии и как tooopt вне его</span><span class="sxs-lookup"><span data-stu-id="aaab3-166">Telemetry data collected and how tooopt out of it</span></span>
<span data-ttu-id="aaab3-167">По умолчанию hello продукта собирает данные телеметрии на hello Service Fabric использования tooimprove hello продукта.</span><span class="sxs-lookup"><span data-stu-id="aaab3-167">As a default, hello product collects telemetry on hello Service Fabric usage tooimprove hello product.</span></span> <span data-ttu-id="aaab3-168">Hello анализатора соответствия рекомендациям, работает как часть установки hello проверяет возможность подключения к слишком[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="aaab3-168">hello Best Practice Analyzer that runs as a part of hello setup checks for connectivity too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="aaab3-169">Если не удается добиться hello программа установки завершается ошибкой, если отказаться телеметрии.</span><span class="sxs-lookup"><span data-stu-id="aaab3-169">If it is not reachable, hello setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="aaab3-170">Hello конвейера телеметрии предпринимает следующие данные слишком hello tooupload[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) один раз в день.</span><span class="sxs-lookup"><span data-stu-id="aaab3-170">hello telemetry pipeline tries tooupload hello following data too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="aaab3-171">Передача усилия и никак не повлияет на функциональные возможности кластера hello.</span><span class="sxs-lookup"><span data-stu-id="aaab3-171">It is a best-effort upload and has no impact on hello cluster functionality.</span></span> <span data-ttu-id="aaab3-172">Данные телеметрии Hello отправляется только из узла "hello" hello, запускается основной диспетчера отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="aaab3-172">hello telemetry is only sent from hello node that runs hello failover manager primary.</span></span> <span data-ttu-id="aaab3-173">С других узлов данные телеметрии не отправляются.</span><span class="sxs-lookup"><span data-stu-id="aaab3-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="aaab3-174">Hello телеметрии состоит из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="aaab3-174">hello telemetry consists of hello following:</span></span>

* <span data-ttu-id="aaab3-175">количество служб;</span><span class="sxs-lookup"><span data-stu-id="aaab3-175">Number of services</span></span>
* <span data-ttu-id="aaab3-176">количество типов служб;</span><span class="sxs-lookup"><span data-stu-id="aaab3-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="aaab3-177">количество приложений;</span><span class="sxs-lookup"><span data-stu-id="aaab3-177">Number of Applications</span></span>
* <span data-ttu-id="aaab3-178">количество обновлений приложений;</span><span class="sxs-lookup"><span data-stu-id="aaab3-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="aaab3-179">количество единиц с отработкой отказа;</span><span class="sxs-lookup"><span data-stu-id="aaab3-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="aaab3-180">количество единиц со встроенной отработкой отказа;</span><span class="sxs-lookup"><span data-stu-id="aaab3-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="aaab3-181">количество единиц с неработоспособной отработкой отказа;</span><span class="sxs-lookup"><span data-stu-id="aaab3-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="aaab3-182">количество реплик;</span><span class="sxs-lookup"><span data-stu-id="aaab3-182">Number of Replicas</span></span>
* <span data-ttu-id="aaab3-183">количество встроенных реплик;</span><span class="sxs-lookup"><span data-stu-id="aaab3-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="aaab3-184">количество реплик в режиме ожидания;</span><span class="sxs-lookup"><span data-stu-id="aaab3-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="aaab3-185">количество автономных реплик;</span><span class="sxs-lookup"><span data-stu-id="aaab3-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="aaab3-186">длина общей очереди;</span><span class="sxs-lookup"><span data-stu-id="aaab3-186">CommonQueueLength</span></span>
* <span data-ttu-id="aaab3-187">длина очереди запросов;</span><span class="sxs-lookup"><span data-stu-id="aaab3-187">QueryQueueLength</span></span>
* <span data-ttu-id="aaab3-188">длина очереди единиц с отработкой отказа;</span><span class="sxs-lookup"><span data-stu-id="aaab3-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="aaab3-189">длина очереди фиксаций;</span><span class="sxs-lookup"><span data-stu-id="aaab3-189">CommitQueueLength</span></span>
* <span data-ttu-id="aaab3-190">количество узлов;</span><span class="sxs-lookup"><span data-stu-id="aaab3-190">Number of Nodes</span></span>
* <span data-ttu-id="aaab3-191">выполнен ли контекст: значение True или False;</span><span class="sxs-lookup"><span data-stu-id="aaab3-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="aaab3-192">идентификатор кластера — это глобальный уникальный идентификатор, который случайным образом формируется для каждого кластера;</span><span class="sxs-lookup"><span data-stu-id="aaab3-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="aaab3-193">версия Service Fabric;</span><span class="sxs-lookup"><span data-stu-id="aaab3-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="aaab3-194">IP-адрес hello виртуальных машин и машин, из какой hello загружается телеметрии</span><span class="sxs-lookup"><span data-stu-id="aaab3-194">IP address of hello virtual machine or machine from which hello telemetry is uploaded</span></span>

<span data-ttu-id="aaab3-195">телеметрии toodisable добавьте hello следующие слишком*свойства* в файле config кластера: *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="aaab3-195">toodisable telemetry, add hello following too*properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="aaab3-196">Возможности на этапе предварительной версии в этом пакете</span><span class="sxs-lookup"><span data-stu-id="aaab3-196">Preview features included in this package</span></span>
<span data-ttu-id="aaab3-197">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="aaab3-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="aaab3-198">Начиная с нового hello [Общедоступной версии hello автономный кластера для Windows Server (версия 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), выпуски toofuture кластера, можно обновить вручную или автоматически.</span><span class="sxs-lookup"><span data-stu-id="aaab3-198">Starting with hello new [GA version of hello standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster toofuture releases, manually or automatically.</span></span> <span data-ttu-id="aaab3-199">См. слишком[обновление кластера Service Fabric автономная версия](service-fabric-cluster-upgrade-windows-server.md) сведения.</span><span class="sxs-lookup"><span data-stu-id="aaab3-199">Refer too[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="aaab3-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aaab3-200">Next steps</span></span>
* [<span data-ttu-id="aaab3-201">Развертывание и удаление приложений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="aaab3-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="aaab3-202">Параметры конфигурации для автономного кластера Windows</span><span class="sxs-lookup"><span data-stu-id="aaab3-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="aaab3-203">Добавление или удаление кластера Service Fabric автономные узлы tooa</span><span class="sxs-lookup"><span data-stu-id="aaab3-203">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* <span data-ttu-id="aaab3-204">[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) (Обновление версии изолированного кластера Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="aaab3-204">[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md)</span></span>
* [<span data-ttu-id="aaab3-205">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server (Создание автономного кластера Service Fabric с тремя узлами на виртуальных машинах Azure под управлением Windows)</span><span class="sxs-lookup"><span data-stu-id="aaab3-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="aaab3-206">Защита автономного кластера под управлением Windows с помощью системы безопасности Windows</span><span class="sxs-lookup"><span data-stu-id="aaab3-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="aaab3-207">Защита автономного кластера под управлением Windows с помощью сертификатов</span><span class="sxs-lookup"><span data-stu-id="aaab3-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
