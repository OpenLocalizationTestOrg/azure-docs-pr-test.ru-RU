---
title: "Настройка изолированного кластера Azure Service Fabric | Документация Майкрософт"
description: "Создание изолированного кластера разработки с тремя узлами, работающими на одном и том же компьютере. После выполнения этого шага вы сможете создавать кластеры с несколькими компьютерами."
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
ms.openlocfilehash: 5c8f4c784eed7b64810a3dd1c36c043d22a66936
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="1c49f-104">Создание первого изолированного кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1c49f-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="1c49f-105">Вы можете создать изолированный кластер Service Fabric на локально или в облаке на виртуальных машинах или компьютерах под управлением Windows Server 2012 R2 или Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="1c49f-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in the cloud.</span></span> <span data-ttu-id="1c49f-106">Это краткое руководство поможет вам создать изолированный кластер разработки в течение нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="1c49f-106">This quickstart helps you to create a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="1c49f-107">Завершив работу с этим руководством, вы получите работающий на отдельном компьютере кластер с тремя узлами, в который вы можете развертывать приложения.</span><span class="sxs-lookup"><span data-stu-id="1c49f-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1c49f-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="1c49f-108">Before you begin</span></span>
<span data-ttu-id="1c49f-109">Service Fabric предоставляет установочный пакет для создания изолированных кластеров Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1c49f-109">Service Fabric provides a setup package to create Service Fabric standalone clusters.</span></span>  <span data-ttu-id="1c49f-110">[Скачайте пакет установки](http://go.microsoft.com/fwlink/?LinkId=730690).</span><span class="sxs-lookup"><span data-stu-id="1c49f-110">[Download the setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="1c49f-111">Распакуйте пакет установки в папку на компьютере или на виртуальной машине, на которой настраивается кластер разработки.</span><span class="sxs-lookup"><span data-stu-id="1c49f-111">Unzip the setup package to a folder on the computer or virtual machine where you are setting up the development cluster.</span></span>  <span data-ttu-id="1c49f-112">Содержимое пакета установки подробно описано [здесь](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="1c49f-112">The contents of the setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="1c49f-113">У администратора кластера, который развертывает и настраивает кластер, должны быть привилегии администратора на компьютере.</span><span class="sxs-lookup"><span data-stu-id="1c49f-113">The cluster administrator deploying and configuring the cluster must have administrator privileges on the computer.</span></span> <span data-ttu-id="1c49f-114">Пакет Service Fabric нельзя установить на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="1c49f-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-the-environment"></a><span data-ttu-id="1c49f-115">Проверка среды</span><span class="sxs-lookup"><span data-stu-id="1c49f-115">Validate the environment</span></span>
<span data-ttu-id="1c49f-116">Скрипт *TestConfiguration.ps1* в изолированном пакете используется как рекомендуемый анализатор, проверяющий возможность развертывания кластера в конкретной среде.</span><span class="sxs-lookup"><span data-stu-id="1c49f-116">The *TestConfiguration.ps1* script in the standalone package is used as a best practices analyzer to validate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="1c49f-117">[Здесь](service-fabric-cluster-standalone-deployment-preparation.md) перечислены предварительные требования к среде при подготовке к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="1c49f-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists the pre-requisites and environment requirements.</span></span> <span data-ttu-id="1c49f-118">Выполните сценарий чтобы проверить, можно ли создать кластер разработки:</span><span class="sxs-lookup"><span data-stu-id="1c49f-118">Run the script to verify if you can create the development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-the-cluster"></a><span data-ttu-id="1c49f-119">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="1c49f-119">Create the cluster</span></span>
<span data-ttu-id="1c49f-120">Некоторые примеры файлов конфигурации кластера устанавливаются с помощью пакета установки.</span><span class="sxs-lookup"><span data-stu-id="1c49f-120">Several sample cluster configuration files are installed with the setup package.</span></span> <span data-ttu-id="1c49f-121">*ClusterConfig.Unsecure.DevCluster.json* — это самая простая конфигурация кластера: незащищенный кластер из трех узлов, работающий на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="1c49f-121">*ClusterConfig.Unsecure.DevCluster.json* is the simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="1c49f-122">Другие файлы конфигурации описывают кластеры с одним или несколькими компьютерами, защищенными с помощью системы безопасности Windows или сертификатов X.509.</span><span class="sxs-lookup"><span data-stu-id="1c49f-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="1c49f-123">Для работы с этим руководством не нужно изменять параметры конфигурации по умолчанию. Просто просмотрите файл конфигурации и ознакомьтесь с параметрами.</span><span class="sxs-lookup"><span data-stu-id="1c49f-123">You don't need to modify any of the default config settings for this tutorial, but look through the config file and get familiar with the settings.</span></span>  <span data-ttu-id="1c49f-124">В разделе **Узлы** описываются три узла в кластере: имя, IP-адрес, а также [тип узла, домен сбоя и обновления](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="1c49f-124">The **nodes** section describes the three nodes in the cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="1c49f-125">В разделе **Свойства** определяются [безопасность, уровень надежности, сбор диагностических сведений и типы узлов](service-fabric-cluster-manifest.md#cluster-properties) для кластера.</span><span class="sxs-lookup"><span data-stu-id="1c49f-125">The **properties** section defines the [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for the cluster.</span></span>

<span data-ttu-id="1c49f-126">Этот кластер не защищен.</span><span class="sxs-lookup"><span data-stu-id="1c49f-126">This cluster is unsecure.</span></span>  <span data-ttu-id="1c49f-127">Любой пользователь может анонимно подключиться и выполнять операции управления, поэтому рабочие кластеры нужно обязательно защищать с помощью сертификатов X.509 или средств обеспечения безопасности Windows.</span><span class="sxs-lookup"><span data-stu-id="1c49f-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="1c49f-128">Безопасность настраивается только во время создания кластера. После этого ее невозможно включить.</span><span class="sxs-lookup"><span data-stu-id="1c49f-128">Security is only configured at cluster creation time and it is not possible to enable security after the cluster is created.</span></span>  <span data-ttu-id="1c49f-129">См. дополнительные сведения о безопасности кластера Service Fabric в статье о [защите кластеров](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="1c49f-129">Read [Secure a cluster](service-fabric-cluster-security.md) to learn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="1c49f-130">Чтобы создать кластер разработки с тремя узлами, запустите скрипт *CreateServiceFabricCluster.ps1* из сеанса PowerShell с правами администратора:</span><span class="sxs-lookup"><span data-stu-id="1c49f-130">To create the three-node development cluster, run the *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="1c49f-131">Пакет среды выполнения Service Fabric автоматически скачивается и устанавливается во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="1c49f-131">The Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="1c49f-132">Подключение к кластеру</span><span class="sxs-lookup"><span data-stu-id="1c49f-132">Connect to the cluster</span></span>
<span data-ttu-id="1c49f-133">Теперь кластер с тремя узлами работает.</span><span class="sxs-lookup"><span data-stu-id="1c49f-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="1c49f-134">Модуль PowerShell ServiceFabric устанавливается вместе со средой выполнения.</span><span class="sxs-lookup"><span data-stu-id="1c49f-134">The ServiceFabric PowerShell module is installed with the runtime.</span></span>  <span data-ttu-id="1c49f-135">Вы можете проверить, работает ли кластер на одном компьютере или на удаленном компьютере со средой выполнения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1c49f-135">You can verify that the cluster is running from the same computer or from a remote computer with the Service Fabric runtime.</span></span>  <span data-ttu-id="1c49f-136">Подключитесь к кластеру, используя командлет [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="1c49f-136">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="1c49f-137">Примеры других способов подключения к кластеру см. в статье о [безопасном подключении к кластеру](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1c49f-137">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="1c49f-138">После подключения к кластеру используйте командлет [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps), чтобы отобразить список узлов в кластере и сведения о состоянии каждого узла.</span><span class="sxs-lookup"><span data-stu-id="1c49f-138">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="1c49f-139">**Состояние работоспособности** каждого узла должно иметь значение *ОК*.</span><span class="sxs-lookup"><span data-stu-id="1c49f-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="1c49f-140">Визуализация кластера с помощью Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="1c49f-140">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="1c49f-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) — хорошее средство для визуализации кластера и управления приложениями.</span><span class="sxs-lookup"><span data-stu-id="1c49f-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="1c49f-142">Service Fabric Explorer — это служба, которая выполняется в кластере. Чтобы получить к ней доступ, перейдите в браузере по адресу [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="1c49f-142">Service Fabric Explorer is a service that runs in the cluster, which you access using a browser by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="1c49f-143">На панели мониторинга кластера представлены общие сведения о кластере, включая общие сведения о приложении и работоспособности узла кластера.</span><span class="sxs-lookup"><span data-stu-id="1c49f-143">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="1c49f-144">В представлении "Узлы" отображается физическая структура кластера.</span><span class="sxs-lookup"><span data-stu-id="1c49f-144">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="1c49f-145">Для каждого узла можно просмотреть, какие приложения были развернуты на этом узле</span><span class="sxs-lookup"><span data-stu-id="1c49f-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-the-cluster"></a><span data-ttu-id="1c49f-147">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="1c49f-147">Remove the cluster</span></span>
<span data-ttu-id="1c49f-148">Чтобы удалить кластер, запустите сценарий Powershell *RemoveServiceFabricCluster.ps1* из папки пакета и передайте в него путь к файлу конфигурации JSON.</span><span class="sxs-lookup"><span data-stu-id="1c49f-148">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="1c49f-149">При необходимости можно указать расположение журнала удаления.</span><span class="sxs-lookup"><span data-stu-id="1c49f-149">You can optionally specify a location for the log of the deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in the configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="1c49f-150">Чтобы удалить среду выполнения Service Fabric с компьютера, выполните следующий скрипт PowerShell из папки пакета.</span><span class="sxs-lookup"><span data-stu-id="1c49f-150">To remove the Service Fabric runtime from the computer, run the following PowerShell script from the package folder.</span></span>

```powershell
# Removes Service Fabric from the current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="1c49f-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c49f-151">Next steps</span></span>
<span data-ttu-id="1c49f-152">Теперь, когда вы настроили изолированный кластер разработки, перейдите к следующим статьям.</span><span class="sxs-lookup"><span data-stu-id="1c49f-152">Now that you have set up a development standalone cluster, try the following articles:</span></span>
* <span data-ttu-id="1c49f-153">[Настройте изолированный кластер с несколькими компьютерами](service-fabric-cluster-creation-for-windows-server.md) и включите режим безопасности.</span><span class="sxs-lookup"><span data-stu-id="1c49f-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="1c49f-154">Разверните приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c49f-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
