---
title: "Добавление узлов к автономному кластеру Service Fabric или удаление узлов из него | Документация Майкрософт"
description: "Узнайте, как добавлять узлы в кластер Azure Service Fabric или удалять их из него на физическом или виртуальном компьютере под управлением Windows Server, расположенном в локальной системе или в любом облаке."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 9c6035e97de38ff63ef074109afd9f3c7484f828
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="add-or-remove-nodes-to-a-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="f3b4e-103">Добавление узлов в автономный кластер Service Fabric под управлением Windows Server или удаление узлов из него</span><span class="sxs-lookup"><span data-stu-id="f3b4e-103">Add or remove nodes to a standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="f3b4e-104">После [создания автономного кластера Service Fabric на компьютерах под управлением Windows Server](service-fabric-cluster-creation-for-windows-server.md) потребности компании могут измениться, и вам может понадобиться добавить или удалить несколько узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need to add or remove nodes to your cluster.</span></span> <span data-ttu-id="f3b4e-105">В данной статье содержатся детальные инструкции по выполнению этой задачи.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-105">This article provides detailed steps to achieve this.</span></span> <span data-ttu-id="f3b4e-106">Обратите внимание, что добавление и удаление узлов в кластерах локальной разработки не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-to-your-cluster"></a><span data-ttu-id="f3b4e-107">Добавление узлов в кластер</span><span class="sxs-lookup"><span data-stu-id="f3b4e-107">Add nodes to your cluster</span></span>
1. <span data-ttu-id="f3b4e-108">Подготовьте виртуальную машину или компьютер, который необходимо добавить в кластер, выполнив действия, описанные в статье [Создание изолированного кластера под управлением Windows Server](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="f3b4e-108">Prepare the VM/machine you want to add to your cluster by following the steps mentioned in the [Prepare the machines to meet the prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="f3b4e-109">Определите, в какой домен сбоя и домен обновления нужно добавить эту виртуальную машину или компьютер.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-109">Identify which fault domain and upgrade domain you are going to add this VM/machine to</span></span>
3. <span data-ttu-id="f3b4e-110">Подключитесь к виртуальной машине или компьютеру, который нужно добавить в кластер, с помощью удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-110">Remote desktop (RDP) into the VM/machine that you want to add to the cluster</span></span>
4. <span data-ttu-id="f3b4e-111">Скопируйте или [скачайте изолированный пакет для Service Fabric для Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) на виртуальную машину или компьютер и извлеките его содержимое.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-111">Copy or [download the standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) to the VM/machine and unzip the package</span></span>
5. <span data-ttu-id="f3b4e-112">Запустите PowerShell с более высоким уровнем привилегий и перейдите к распакованному пакету.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-112">Run Powershell with elevated privileges, and navigate to the location of the unzipped package</span></span>
6. <span data-ttu-id="f3b4e-113">Запустите скрипт *AddNode.ps1*, указав параметры, описывающие новый узел, который будет добавлен.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-113">Run the *AddNode.ps1* script with the parameters describing the new node to add.</span></span> <span data-ttu-id="f3b4e-114">В этом примере добавляется новый узел с именем VM5, типом NodeType0, IP-адресом 182.17.34.52 и UD1 со значением fd:/dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-114">The example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="f3b4e-115">*ExistingClusterConnectionEndPoint* — это конечная точка подключения для узла в имеющемся кластере, который может содержать IP-адрес *любого* узла в этом кластере.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-115">The *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in the existing cluster, which can be the IP address of *any* node in the cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="f3b4e-116">После выполнения скрипта можно проверить, добавлен ли новый узел, выполнив командлет [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f3b4e-116">Once the script finishes running, you can check if the new node has been added by running the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="f3b4e-117">Чтобы обеспечить согласованность на различных узлах в кластере, нужно обновить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-117">To ensure consistency across different nodes in the cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="f3b4e-118">Выполните команду [Get- ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps), чтобы получить самый последний файл конфигурации, и добавьте вновь добавленный узел в раздел узлов.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and add the newly added node to "Nodes" section.</span></span> <span data-ttu-id="f3b4e-119">Кроме того, мы рекомендуем всегда иметь под рукой последнюю конфигурацию кластера, если вам понадобится развернуть кластер с той же конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-119">It is also recommended to always have the latest cluster configuration available in the case that you need to redploy a cluster with the same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="f3b4e-120">Выполните команду [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps), чтобы начать обновление.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="f3b4e-121">Ход выполнения обновления можно отслеживать с помощью Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-121">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="f3b4e-122">Кроме того, с этой же целью можно выполнить команду [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f3b4e-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-to-clusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="f3b4e-123">Добавление узлов в кластеры, настроенные с помощью Windows Security, с использованием gMSA</span><span class="sxs-lookup"><span data-stu-id="f3b4e-123">Add nodes to clusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="f3b4e-124">Для кластеров, настроенных с помощью групповой управляемой учетной записи службы (https://technet.microsoft.com/library/hh831782.aspx), можно добавить новый узел, используя обновление конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="f3b4e-125">Выполните команду [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) на любом из имеющихся узлов, чтобы получить самый последний файл конфигурации, и добавьте сведения о новом узле, который нужно добавить в раздел узлов.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of the existing nodes to get the latest configuration file and add details about the new node you want to add in the "Nodes" section.</span></span> <span data-ttu-id="f3b4e-126">Убедитесь, что новый узел входит в ту же учетную запись, которой управляет группа.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-126">Make sure the new node is part of the same group managed account.</span></span> <span data-ttu-id="f3b4e-127">Этой учетной записи нужно назначить роль "Администратор" на всех компьютерах.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="f3b4e-128">Выполните команду [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps), чтобы начать обновление.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>
    ```
    <span data-ttu-id="f3b4e-129">Ход выполнения обновления можно отслеживать с помощью Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-129">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="f3b4e-130">Кроме того, с этой же целью можно выполнить команду [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f3b4e-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-to-your-cluster"></a><span data-ttu-id="f3b4e-131">Добавление типов узлов в кластер</span><span class="sxs-lookup"><span data-stu-id="f3b4e-131">Add node types to your cluster</span></span>
<span data-ttu-id="f3b4e-132">Чтобы добавить новый тип узла, измените конфигурацию, чтобы добавить новый тип узла в разделе NodeTypes в области Properties, и начните обновление конфигурации, используя [ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f3b4e-132">In order to add a new node type, modify your configuration to include the new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="f3b4e-133">После завершения обновления в кластер можно добавить новые узлы этого типа.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-133">Once the upgrade completes, you can add new nodes to your cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="f3b4e-134">Удаление узлов из кластера</span><span class="sxs-lookup"><span data-stu-id="f3b4e-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="f3b4e-135">Вы можете удалить узел из кластера в ходе обновления конфигурации следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f3b4e-135">A node can be removed from a cluster using a configuration upgrade, in the following manner:</span></span>

1. <span data-ttu-id="f3b4e-136">Выполните команду [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps), чтобы получить последний файл конфигурации, и *удалите* узел из раздела узлов.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and *remove* the node from "Nodes" section.</span></span>
<span data-ttu-id="f3b4e-137">Добавьте параметр NodesToBeRemoved в раздел Setup в разделе FabricSettings.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-137">Add the "NodesToBeRemoved" parameter to "Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="f3b4e-138">В качестве значений следует использовать разделенный запятыми список узлов, которые необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-138">The "value" should be a comma separated list of node names of nodes that need to be removed.</span></span>

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. <span data-ttu-id="f3b4e-139">Выполните команду [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps), чтобы начать обновление.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="f3b4e-140">Ход выполнения обновления можно отслеживать с помощью Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-140">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="f3b4e-141">Кроме того, с этой же целью можно выполнить команду [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f3b4e-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="f3b4e-142">При удалении узлов может выполниться несколько обновлений.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="f3b4e-143">Некоторые узлы будут отмечены тегом `IsSeedNode=”true”`. Их можно определить, запросив манифест кластера с использованием `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying the cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="f3b4e-144">Удаление таких узлов может занимать больше времени, чем других, так как в таких сценариях начальные узлы придется перемещать.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-144">Removal of such nodes may take longer than others since the seed nodes will have to be moved around in such scenarios.</span></span> <span data-ttu-id="f3b4e-145">Кластер должен поддерживать как минимум 3 первичных узла.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-145">The cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="f3b4e-146">Удаление типов узлов из кластера</span><span class="sxs-lookup"><span data-stu-id="f3b4e-146">Remove node types from your cluster</span></span>
<span data-ttu-id="f3b4e-147">Прежде чем удалить тип узла, перепроверьте, нет ли узлов, которые ссылаются на этот тип.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-147">Before removing a node type, please double check if there are any nodes referencing the node type.</span></span> <span data-ttu-id="f3b4e-148">Перед удалением соответствующего типа узла удалите эти узлы.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-148">Remove these nodes before removing the corresponding node type.</span></span> <span data-ttu-id="f3b4e-149">После удаления всех соответствующих узлов NodeType можно удалить из конфигурации кластера и начать обновление конфигурации с помощью [ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f3b4e-149">Once all corresponding nodes are removed, you can remove the NodeType from the cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="f3b4e-150">Замена основных узлов кластера</span><span class="sxs-lookup"><span data-stu-id="f3b4e-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="f3b4e-151">Замену основных узлов следует выполнять последовательно, вместо того чтобы удалять, а затем добавлять их массово.</span><span class="sxs-lookup"><span data-stu-id="f3b4e-151">The replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f3b4e-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f3b4e-152">Next steps</span></span>
* [<span data-ttu-id="f3b4e-153">Параметры конфигурации для автономного кластера Windows</span><span class="sxs-lookup"><span data-stu-id="f3b4e-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="f3b4e-154">Защита автономного кластера под управлением Windows с помощью сертификатов</span><span class="sxs-lookup"><span data-stu-id="f3b4e-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="f3b4e-155">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server (Создание автономного кластера Service Fabric с тремя узлами на виртуальных машинах Azure под управлением Windows)</span><span class="sxs-lookup"><span data-stu-id="f3b4e-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

