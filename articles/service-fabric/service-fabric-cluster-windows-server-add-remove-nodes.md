---
title: "aaaAdd или удаление кластера Service Fabric узлы tooa автономный | Документы Microsoft"
description: "Узнайте, как tooadd или удалите tooan узлы Azure Service Fabric кластера на физическом компьютере или виртуальной машине под управлением Windows Server, которая может быть локальной или в любом облаке."
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
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="ad510-103">Добавление или удаление узлов tooa автономный Service Fabric кластера под управлением Windows Server</span><span class="sxs-lookup"><span data-stu-id="ad510-103">Add or remove nodes tooa standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="ad510-104">После того как вы [кластер Service Fabric автономный создан на компьютерах Windows Server](service-fabric-cluster-creation-for-windows-server.md), могут изменяться вашим потребностям и может потребоваться tooadd или удаления узлов кластера tooyour.</span><span class="sxs-lookup"><span data-stu-id="ad510-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need tooadd or remove nodes tooyour cluster.</span></span> <span data-ttu-id="ad510-105">Эта статья содержит подробные инструкции tooachieve это.</span><span class="sxs-lookup"><span data-stu-id="ad510-105">This article provides detailed steps tooachieve this.</span></span> <span data-ttu-id="ad510-106">Обратите внимание, что добавление и удаление узлов в кластерах локальной разработки не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ad510-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-tooyour-cluster"></a><span data-ttu-id="ad510-107">Добавление узлов кластера tooyour</span><span class="sxs-lookup"><span data-stu-id="ad510-107">Add nodes tooyour cluster</span></span>
1. <span data-ttu-id="ad510-108">Hello подготовки виртуальной Машины или компьютер, tooadd tooyour кластера hello выполните действия, упомянутые в hello [hello Подготовка компьютеров для развертывания кластера компоненты hello toomeet](service-fabric-cluster-creation-for-windows-server.md) раздела</span><span class="sxs-lookup"><span data-stu-id="ad510-108">Prepare hello VM/machine you want tooadd tooyour cluster by following hello steps mentioned in hello [Prepare hello machines toomeet hello prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="ad510-109">Определите, какой домен сбоя и домен обновления являются постоянной tooadd этой виртуальной Машины и машины</span><span class="sxs-lookup"><span data-stu-id="ad510-109">Identify which fault domain and upgrade domain you are going tooadd this VM/machine to</span></span>
3. <span data-ttu-id="ad510-110">Удаленного рабочего стола (RDP) к hello виртуальной Машины или компьютер, что tooadd toohello кластера</span><span class="sxs-lookup"><span data-stu-id="ad510-110">Remote desktop (RDP) into hello VM/machine that you want tooadd toohello cluster</span></span>
4. <span data-ttu-id="ad510-111">Копирование или [загрузить hello изолированный пакет для структуры службы Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello ВМ/machine и распакуйте пакет hello</span><span class="sxs-lookup"><span data-stu-id="ad510-111">Copy or [download hello standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine and unzip hello package</span></span>
5. <span data-ttu-id="ad510-112">Запустите Powershell с повышенными привилегиями и перейдите в расположение toohello hello распакованную пакета</span><span class="sxs-lookup"><span data-stu-id="ad510-112">Run Powershell with elevated privileges, and navigate toohello location of hello unzipped package</span></span>
6. <span data-ttu-id="ad510-113">Запустите hello *AddNode.ps1* сценария с параметрами hello, описывающие новый узел tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="ad510-113">Run hello *AddNode.ps1* script with hello parameters describing hello new node tooadd.</span></span> <span data-ttu-id="ad510-114">Приведенный ниже пример Hello добавляет новый узел с именем VM5, с типом NodeType0 и IP-адрес 182.17.34.52, UD1 и fd: / dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="ad510-114">hello example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="ad510-115">Hello *ExistingClusterConnectionEndPoint* уже конечная точка подключения для узла в существующий кластер hello, которой может быть IP-адрес hello *любой* узла в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="ad510-115">hello *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in hello existing cluster, which can be hello IP address of *any* node in hello cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="ad510-116">Когда сценарий hello завершает работу, можно проверить, добавлен ли hello новый узел, выполнив hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="ad510-116">Once hello script finishes running, you can check if hello new node has been added by running hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="ad510-117">tooensure согласованности на разных узлах кластера hello, необходимо произвести обновление конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ad510-117">tooensure consistency across different nodes in hello cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="ad510-118">Запустите [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello последний файл конфигурации и добавить hello вновь добавленный узел слишком раздел «Узлы».</span><span class="sxs-lookup"><span data-stu-id="ad510-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and add hello newly added node too"Nodes" section.</span></span> <span data-ttu-id="ad510-119">Также рекомендуется tooalways есть hello последняя конфигурация кластера в случае hello необходимые tooredploy кластер с hello одной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ad510-119">It is also recommended tooalways have hello latest cluster configuration available in hello case that you need tooredploy a cluster with hello same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="ad510-120">Запустите [ServiceFabricClusterConfigurationUpgrade начала](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello обновления.</span><span class="sxs-lookup"><span data-stu-id="ad510-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="ad510-121">Можно отслеживать ход выполнения обновления hello на Service Fabric Explorer hello.</span><span class="sxs-lookup"><span data-stu-id="ad510-121">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="ad510-122">Кроме того, с этой же целью можно выполнить команду [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="ad510-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="ad510-123">Добавление tooclusters узлов, настроенного с использованием групповой управляемой учетной записи Windows</span><span class="sxs-lookup"><span data-stu-id="ad510-123">Add nodes tooclusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="ad510-124">Для кластеров, настроенных с помощью групповой управляемой учетной записи службы (https://technet.microsoft.com/library/hh831782.aspx), можно добавить новый узел, используя обновление конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ad510-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="ad510-125">Запустите [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) на любом из существующих узлов hello tooget hello последний файл конфигурации и добавление сведений об о hello нового узла требуется tooadd раздела узлов «hello».</span><span class="sxs-lookup"><span data-stu-id="ad510-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of hello existing nodes tooget hello latest configuration file and add details about hello new node you want tooadd in hello "Nodes" section.</span></span> <span data-ttu-id="ad510-126">Убедитесь, что новый узел hello входит в состав hello же группы управляемую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ad510-126">Make sure hello new node is part of hello same group managed account.</span></span> <span data-ttu-id="ad510-127">Этой учетной записи нужно назначить роль "Администратор" на всех компьютерах.</span><span class="sxs-lookup"><span data-stu-id="ad510-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="ad510-128">Запустите [ServiceFabricClusterConfigurationUpgrade начала](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello обновления.</span><span class="sxs-lookup"><span data-stu-id="ad510-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    <span data-ttu-id="ad510-129">Можно отслеживать ход выполнения обновления hello на Service Fabric Explorer hello.</span><span class="sxs-lookup"><span data-stu-id="ad510-129">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="ad510-130">Кроме того, с этой же целью можно выполнить команду [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="ad510-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-tooyour-cluster"></a><span data-ttu-id="ad510-131">Добавление узла типы tooyour кластера</span><span class="sxs-lookup"><span data-stu-id="ad510-131">Add node types tooyour cluster</span></span>
<span data-ttu-id="ad510-132">В заказ tooadd нового типа узлов, изменить вашей конфигурации tooinclude hello новый тип узла в разделе «NodeTypes» в разделе «Свойства» и начать настройку обновление с помощью [ServiceFabricClusterConfigurationUpgrade начала](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="ad510-132">In order tooadd a new node type, modify your configuration tooinclude hello new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="ad510-133">После завершения обновления hello, можно добавить новый кластер tooyour узлы с этим типом узла.</span><span class="sxs-lookup"><span data-stu-id="ad510-133">Once hello upgrade completes, you can add new nodes tooyour cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="ad510-134">Удаление узлов из кластера</span><span class="sxs-lookup"><span data-stu-id="ad510-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="ad510-135">Можно удалить узел из кластера с помощью обновления конфигурации в следующих способом hello:</span><span class="sxs-lookup"><span data-stu-id="ad510-135">A node can be removed from a cluster using a configuration upgrade, in hello following manner:</span></span>

1. <span data-ttu-id="ad510-136">Запустите [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello последний файл конфигурации и *удалить* hello узел из раздела «Узлов».</span><span class="sxs-lookup"><span data-stu-id="ad510-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and *remove* hello node from "Nodes" section.</span></span>
<span data-ttu-id="ad510-137">Добавить hello «NodesToBeRemoved» параметр слишком «Setup» раздел в разделе «FabricSettings».</span><span class="sxs-lookup"><span data-stu-id="ad510-137">Add hello "NodesToBeRemoved" parameter too"Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="ad510-138">Hello «value» должно быть разделенный запятыми список имен узлов, узлов, которые требуется удалить toobe.</span><span class="sxs-lookup"><span data-stu-id="ad510-138">hello "value" should be a comma separated list of node names of nodes that need toobe removed.</span></span>

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
2. <span data-ttu-id="ad510-139">Запустите [ServiceFabricClusterConfigurationUpgrade начала](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello обновления.</span><span class="sxs-lookup"><span data-stu-id="ad510-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="ad510-140">Можно отслеживать ход выполнения обновления hello на Service Fabric Explorer hello.</span><span class="sxs-lookup"><span data-stu-id="ad510-140">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="ad510-141">Кроме того, с этой же целью можно выполнить команду [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="ad510-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="ad510-142">При удалении узлов может выполниться несколько обновлений.</span><span class="sxs-lookup"><span data-stu-id="ad510-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="ad510-143">Некоторые узлы будут отмечены `IsSeedNode=”true”` тега и могут быть идентифицированы с помощью запроса к кластеру hello манифеста с помощью `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="ad510-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying hello cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="ad510-144">Удаление таких узлов может потребоваться дольше, чем другие, поскольку узлы hello начальное значение будет иметь toobe перемещаются в таких сценариях.</span><span class="sxs-lookup"><span data-stu-id="ad510-144">Removal of such nodes may take longer than others since hello seed nodes will have toobe moved around in such scenarios.</span></span> <span data-ttu-id="ad510-145">Hello кластера должен поддерживать как минимум 3 узлы типа первичного узла.</span><span class="sxs-lookup"><span data-stu-id="ad510-145">hello cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="ad510-146">Удаление типов узлов из кластера</span><span class="sxs-lookup"><span data-stu-id="ad510-146">Remove node types from your cluster</span></span>
<span data-ttu-id="ad510-147">Перед удалением типа узла, проверьте правильность, если все узлы, ссылающимся на тип узла hello.</span><span class="sxs-lookup"><span data-stu-id="ad510-147">Before removing a node type, please double check if there are any nodes referencing hello node type.</span></span> <span data-ttu-id="ad510-148">Удалите эти узлы перед удалением hello соответствующий тип узла.</span><span class="sxs-lookup"><span data-stu-id="ad510-148">Remove these nodes before removing hello corresponding node type.</span></span> <span data-ttu-id="ad510-149">После удаления всех соответствующих узлов можно удалить hello NodeType из конфигурации кластера hello и начать настройку обновление с помощью [ServiceFabricClusterConfigurationUpgrade начала](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="ad510-149">Once all corresponding nodes are removed, you can remove hello NodeType from hello cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="ad510-150">Замена основных узлов кластера</span><span class="sxs-lookup"><span data-stu-id="ad510-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="ad510-151">Hello замены основного узлов должно быть выполнено одного узла за другим, а не удалите и добавьте их в пакетах.</span><span class="sxs-lookup"><span data-stu-id="ad510-151">hello replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ad510-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad510-152">Next steps</span></span>
* [<span data-ttu-id="ad510-153">Параметры конфигурации для автономного кластера Windows</span><span class="sxs-lookup"><span data-stu-id="ad510-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="ad510-154">Защита автономного кластера под управлением Windows с помощью сертификатов</span><span class="sxs-lookup"><span data-stu-id="ad510-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="ad510-155">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server (Создание автономного кластера Service Fabric с тремя узлами на виртуальных машинах Azure под управлением Windows)</span><span class="sxs-lookup"><span data-stu-id="ad510-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

