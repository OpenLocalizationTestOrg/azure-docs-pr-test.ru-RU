---
title: "aaaSet кластера Azure Service Fabric автономный | Документы Microsoft"
description: "Создание кластера автономный разработки с тремя узлами под управлением hello того же компьютера. После завершения этой установки, будет готов toocreate кластер с несколькими компьютерами."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="e6b26-104">Создание первого изолированного кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e6b26-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="e6b26-105">Можно создать автономный кластера Service Fabric на виртуальные машины или компьютеры под управлением Windows Server 2012 R2 или Windows Server 2016 в локальной среде или в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="e6b26-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in hello cloud.</span></span> <span data-ttu-id="e6b26-106">Краткого руководства помогает toocreate кластера автономный разработки только через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e6b26-106">This quickstart helps you toocreate a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="e6b26-107">Завершив работу с этим руководством, вы получите работающий на отдельном компьютере кластер с тремя узлами, в который вы можете развертывать приложения.</span><span class="sxs-lookup"><span data-stu-id="e6b26-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e6b26-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e6b26-108">Before you begin</span></span>
<span data-ttu-id="e6b26-109">Service Fabric предоставляет программу установки пакета toocreate Service Fabric изолированные кластеры.</span><span class="sxs-lookup"><span data-stu-id="e6b26-109">Service Fabric provides a setup package toocreate Service Fabric standalone clusters.</span></span>  <span data-ttu-id="e6b26-110">[Скачайте пакет установки hello](http://go.microsoft.com/fwlink/?LinkId=730690).</span><span class="sxs-lookup"><span data-stu-id="e6b26-110">[Download hello setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="e6b26-111">Распакуйте hello установки tooa папку пакета в hello компьютер или виртуальную машину где вы настраиваете кластеру разработки hello.</span><span class="sxs-lookup"><span data-stu-id="e6b26-111">Unzip hello setup package tooa folder on hello computer or virtual machine where you are setting up hello development cluster.</span></span>  <span data-ttu-id="e6b26-112">подробно описаны Hello содержимое пакета установки hello [здесь](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="e6b26-112">hello contents of hello setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="e6b26-113">Администратор кластера Hello, развертыванию и настройке кластера hello требуются права администратора на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="e6b26-113">hello cluster administrator deploying and configuring hello cluster must have administrator privileges on hello computer.</span></span> <span data-ttu-id="e6b26-114">Пакет Service Fabric нельзя установить на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="e6b26-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-hello-environment"></a><span data-ttu-id="e6b26-115">Проверка среды hello</span><span class="sxs-lookup"><span data-stu-id="e6b26-115">Validate hello environment</span></span>
<span data-ttu-id="e6b26-116">Hello *TestConfiguration.ps1* сценарий в hello изолированный пакет используется в качестве наиболее toovalidate анализатора соответствия рекомендациям ли кластер может быть развернут в данной среде.</span><span class="sxs-lookup"><span data-stu-id="e6b26-116">hello *TestConfiguration.ps1* script in hello standalone package is used as a best practices analyzer toovalidate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="e6b26-117">[Подготовка к развертыванию](service-fabric-cluster-standalone-deployment-preparation.md) hello перечислены необходимые условия и требования к среде.</span><span class="sxs-lookup"><span data-stu-id="e6b26-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists hello pre-requisites and environment requirements.</span></span> <span data-ttu-id="e6b26-118">Выполните сценарий tooverify hello при создании кластера hello разработки:</span><span class="sxs-lookup"><span data-stu-id="e6b26-118">Run hello script tooverify if you can create hello development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a><span data-ttu-id="e6b26-119">Создание кластера hello</span><span class="sxs-lookup"><span data-stu-id="e6b26-119">Create hello cluster</span></span>
<span data-ttu-id="e6b26-120">Некоторые примеры файлов конфигурации кластера устанавливаются вместе с hello пакета установки.</span><span class="sxs-lookup"><span data-stu-id="e6b26-120">Several sample cluster configuration files are installed with hello setup package.</span></span> <span data-ttu-id="e6b26-121">*ClusterConfig.Unsecure.DevCluster.json* — простая конфигурация кластера hello: небезопасным, трех узлов кластера, работающих на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="e6b26-121">*ClusterConfig.Unsecure.DevCluster.json* is hello simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="e6b26-122">Другие файлы конфигурации описывают кластеры с одним или несколькими компьютерами, защищенными с помощью системы безопасности Windows или сертификатов X.509.</span><span class="sxs-lookup"><span data-stu-id="e6b26-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="e6b26-123">Не требуется toomodify ни один из параметров конфигурации по умолчанию hello в этом учебнике, но просмотрите файл конфигурации hello и ознакомиться с параметрами hello.</span><span class="sxs-lookup"><span data-stu-id="e6b26-123">You don't need toomodify any of hello default config settings for this tutorial, but look through hello config file and get familiar with hello settings.</span></span>  <span data-ttu-id="e6b26-124">Hello **узлы** разделе описываются hello три узла в кластере hello: имя, IP-адрес [тип узла, домен сбоя и домен обновления](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="e6b26-124">hello **nodes** section describes hello three nodes in hello cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="e6b26-125">Hello **свойства** раздел определяет hello [безопасности, уровень надежности, сбор диагностических сведений и типы узлов](service-fabric-cluster-manifest.md#cluster-properties) для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="e6b26-125">hello **properties** section defines hello [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for hello cluster.</span></span>

<span data-ttu-id="e6b26-126">Этот кластер не защищен.</span><span class="sxs-lookup"><span data-stu-id="e6b26-126">This cluster is unsecure.</span></span>  <span data-ttu-id="e6b26-127">Любой пользователь может анонимно подключиться и выполнять операции управления, поэтому рабочие кластеры нужно обязательно защищать с помощью сертификатов X.509 или средств обеспечения безопасности Windows.</span><span class="sxs-lookup"><span data-stu-id="e6b26-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="e6b26-128">Во время создания кластера только настройки безопасности и не возможные tooenable безопасности после создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e6b26-128">Security is only configured at cluster creation time and it is not possible tooenable security after hello cluster is created.</span></span>  <span data-ttu-id="e6b26-129">Чтение [защиты кластера](service-fabric-cluster-security.md) toolearn Дополнительные сведения о безопасности кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e6b26-129">Read [Secure a cluster](service-fabric-cluster-security.md) toolearn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="e6b26-130">toocreate hello разработки трех узлов кластера, запустите hello *CreateServiceFabricCluster.ps1* сценарий из сеанса PowerShell администратора:</span><span class="sxs-lookup"><span data-stu-id="e6b26-130">toocreate hello three-node development cluster, run hello *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="e6b26-131">пакет среды выполнения Service Fabric Hello автоматически загружаются и устанавливаются во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="e6b26-131">hello Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="e6b26-132">Подключите кластер toohello</span><span class="sxs-lookup"><span data-stu-id="e6b26-132">Connect toohello cluster</span></span>
<span data-ttu-id="e6b26-133">Теперь кластер с тремя узлами работает.</span><span class="sxs-lookup"><span data-stu-id="e6b26-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="e6b26-134">Hello модуля ServiceFabric PowerShell устанавливается вместе с hello среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="e6b26-134">hello ServiceFabric PowerShell module is installed with hello runtime.</span></span>  <span data-ttu-id="e6b26-135">Можно проверить этот кластер hello выполняется с hello же компьютере или на удаленном компьютере со средой выполнения Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="e6b26-135">You can verify that hello cluster is running from hello same computer or from a remote computer with hello Service Fabric runtime.</span></span>  <span data-ttu-id="e6b26-136">Hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлет устанавливает toohello подключения кластера.</span><span class="sxs-lookup"><span data-stu-id="e6b26-136">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="e6b26-137">В разделе [кластера безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md) другие примеры соединения tooa кластера.</span><span class="sxs-lookup"><span data-stu-id="e6b26-137">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="e6b26-138">После подключения кластера toohello, используйте hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay командлет список узлов в hello сведения о кластере и состоянии для каждого узла.</span><span class="sxs-lookup"><span data-stu-id="e6b26-138">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="e6b26-139">**Состояние работоспособности** каждого узла должно иметь значение *ОК*.</span><span class="sxs-lookup"><span data-stu-id="e6b26-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="e6b26-140">Визуализация hello кластера с помощью обозревателя Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e6b26-140">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="e6b26-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) — хорошее средство для визуализации кластера и управления приложениями.</span><span class="sxs-lookup"><span data-stu-id="e6b26-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="e6b26-142">Обозреватель Service Fabric — это служба, который работает в кластере hello, доступ к которому осуществляется с помощью браузера, перейдя по слишком[http://localhost:19080/обозреватель](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="e6b26-142">Service Fabric Explorer is a service that runs in hello cluster, which you access using a browser by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="e6b26-143">панели мониторинга кластера Hello Обзор кластера, в том числе сводную приложения и состояние работоспособности узла.</span><span class="sxs-lookup"><span data-stu-id="e6b26-143">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="e6b26-144">представление узла Hello отображает hello физическую структуру hello кластера.</span><span class="sxs-lookup"><span data-stu-id="e6b26-144">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="e6b26-145">Для каждого узла можно просмотреть, какие приложения были развернуты на этом узле</span><span class="sxs-lookup"><span data-stu-id="e6b26-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a><span data-ttu-id="e6b26-147">Удаление кластера hello</span><span class="sxs-lookup"><span data-stu-id="e6b26-147">Remove hello cluster</span></span>
<span data-ttu-id="e6b26-148">tooremove кластера, запустите hello *RemoveServiceFabricCluster.ps1* сценарий PowerShell из папки пакета hello и передайте его в файл конфигурации JSON toohello путь hello.</span><span class="sxs-lookup"><span data-stu-id="e6b26-148">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="e6b26-149">При необходимости можно указать расположение для журнала hello hello операции удаления.</span><span class="sxs-lookup"><span data-stu-id="e6b26-149">You can optionally specify a location for hello log of hello deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="e6b26-150">tooremove hello среда выполнения Service Fabric с компьютера hello, запустите следующий сценарий PowerShell из папки пакета hello hello.</span><span class="sxs-lookup"><span data-stu-id="e6b26-150">tooremove hello Service Fabric runtime from hello computer, run hello following PowerShell script from hello package folder.</span></span>

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="e6b26-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e6b26-151">Next steps</span></span>
<span data-ttu-id="e6b26-152">Теперь, когда настраивается кластер автономный разработки, попробуйте hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="e6b26-152">Now that you have set up a development standalone cluster, try hello following articles:</span></span>
* <span data-ttu-id="e6b26-153">[Настройте изолированный кластер с несколькими компьютерами](service-fabric-cluster-creation-for-windows-server.md) и включите режим безопасности.</span><span class="sxs-lookup"><span data-stu-id="e6b26-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="e6b26-154">Разверните приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6b26-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
