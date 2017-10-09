---
title: "aaaConfigure кластера автономной Azure Service Fabric | Документы Microsoft"
description: "Узнайте, как tooconfigure изолированном или закрытый кластера Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="59e8f-103">Параметры конфигурации для автономного кластера Windows</span><span class="sxs-lookup"><span data-stu-id="59e8f-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="59e8f-104">В этой статье описывается, как hello кластера Service Fabric автономный заданий с помощью tooconfigure ***ClusterConfig.JSON*** файла.</span><span class="sxs-lookup"><span data-stu-id="59e8f-104">This article describes how tooconfigure a standalone Service Fabric cluster using hello ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="59e8f-105">Можно использовать этот файл toospecify сведения hello Service Fabric узлов и IP-адресов, различные типы узлов кластера hello, hello конфигурации безопасности, а также hello топологии сети с точки зрения домены сбоя и обновления для вашего автономного кластер.</span><span class="sxs-lookup"><span data-stu-id="59e8f-105">You can use this file toospecify information such as hello Service Fabric nodes and their IP addresses, different types of nodes on hello cluster, hello security configurations as well as hello network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="59e8f-106">При вы [загрузить hello изолированный пакет Service Fabric](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), несколько образцов hello ClusterConfig.JSON файла при отсутствии загруженных tooyour работы.</span><span class="sxs-lookup"><span data-stu-id="59e8f-106">When you [download hello standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of hello ClusterConfig.JSON file are downloaded tooyour work machine.</span></span> <span data-ttu-id="59e8f-107">образцы Hello наличие *DevCluster* в именах поможет вам создать кластер с тремя узлами на hello же компьютера, такие как логические узлы.</span><span class="sxs-lookup"><span data-stu-id="59e8f-107">hello samples having *DevCluster* in their names will help you create a cluster with all three nodes on hello same machine, like logical nodes.</span></span> <span data-ttu-id="59e8f-108">По крайней мере один узел должен быть помечен как первичный.</span><span class="sxs-lookup"><span data-stu-id="59e8f-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="59e8f-109">Данный кластер удобен для среды разработки или тестирования, но не предназначен для использования в качестве рабочего кластера.</span><span class="sxs-lookup"><span data-stu-id="59e8f-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="59e8f-110">образцы Hello наличие *MultiMachine* в именах, поможет вам создать кластер производственного качества, с каждым узлом на отдельном компьютере.</span><span class="sxs-lookup"><span data-stu-id="59e8f-110">hello samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="59e8f-111">*ClusterConfig.Unsecure.DevCluster.JSON* и *ClusterConfig.Unsecure.MultiMachine.JSON* Показать, как toocreate небезопасные тестирования или производственных кластера соответственно.</span><span class="sxs-lookup"><span data-stu-id="59e8f-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how toocreate an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="59e8f-112">*ClusterConfig.Windows.DevCluster.JSON* и *ClusterConfig.Windows.MultiMachine.JSON* Показать, как toocreate или тестовом кластера защищено с помощью [безопасности Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="59e8f-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how toocreate test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="59e8f-113">*ClusterConfig.X509.DevCluster.JSON* и *ClusterConfig.X509.MultiMachine.JSON* Показать, как toocreate или тестовом кластера защищено с помощью [X509 безопасности на основе сертификатов](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="59e8f-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how toocreate test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="59e8f-114">Теперь рассмотрим hello различные разделы ***ClusterConfig.JSON*** файла, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="59e8f-114">Now we will examine hello various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="59e8f-115">Общие параметры кластера</span><span class="sxs-lookup"><span data-stu-id="59e8f-115">General cluster configurations</span></span>
<span data-ttu-id="59e8f-116">Они охватывают hello широкий определенной конфигурации кластера, как показано в приведенном ниже фрагменте JSON hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-116">This covers hello broad cluster specific configurations, as shown in hello JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="59e8f-117">Можно присвоить понятное имя кластера Service Fabric tooyour назначив toohello **имя** переменной.</span><span class="sxs-lookup"><span data-stu-id="59e8f-117">You can give any friendly name tooyour Service Fabric cluster by assigning it toohello **name** variable.</span></span> <span data-ttu-id="59e8f-118">Hello **clusterConfigurationVersion** — номер версии hello кластера; следует увеличить ее каждый раз, чтобы обновить кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="59e8f-118">hello **clusterConfigurationVersion** is hello version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="59e8f-119">Однако следует оставить hello **apiVersion** toohello значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="59e8f-119">You should however leave hello **apiVersion** toohello default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a><span data-ttu-id="59e8f-120">Узлы в кластере hello</span><span class="sxs-lookup"><span data-stu-id="59e8f-120">Nodes on hello cluster</span></span>
<span data-ttu-id="59e8f-121">Можно настроить hello узлы в кластере Service Fabric с помощью hello **узлы** раздел, в следующем фрагменте кода показан hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-121">You can configure hello nodes on your Service Fabric cluster by using hello **nodes** section, as hello following snippet shows.</span></span>

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

<span data-ttu-id="59e8f-122">Кластер Service Fabric должен содержать по крайней мере 3 узла.</span><span class="sxs-lookup"><span data-stu-id="59e8f-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="59e8f-123">Можно добавить дополнительные узлы toothis раздел согласно настройки программы установки.</span><span class="sxs-lookup"><span data-stu-id="59e8f-123">You can add more nodes toothis section as per your setup.</span></span> <span data-ttu-id="59e8f-124">Hello в следующей таблице описывается hello параметры конфигурации для каждого узла.</span><span class="sxs-lookup"><span data-stu-id="59e8f-124">hello following table explains hello configuration settings for each node.</span></span>

| <span data-ttu-id="59e8f-125">**Параметр узла**</span><span class="sxs-lookup"><span data-stu-id="59e8f-125">**Node configuration**</span></span> | <span data-ttu-id="59e8f-126">**Описание**</span><span class="sxs-lookup"><span data-stu-id="59e8f-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="59e8f-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="59e8f-127">nodeName</span></span> |<span data-ttu-id="59e8f-128">Можно присвоить любой узел toohello понятное имя.</span><span class="sxs-lookup"><span data-stu-id="59e8f-128">You can give any friendly name toohello node.</span></span> |
| <span data-ttu-id="59e8f-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="59e8f-129">iPAddress</span></span> |<span data-ttu-id="59e8f-130">Узнать hello IP-адрес вашего узла, откройте окно командной строки и введите `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="59e8f-130">Find out hello IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="59e8f-131">Записать hello IPV4-адрес и назначьте его toohello **IP-адрес** переменной.</span><span class="sxs-lookup"><span data-stu-id="59e8f-131">Note hello IPV4 address and assign it toohello **iPAddress** variable.</span></span> |
| <span data-ttu-id="59e8f-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="59e8f-132">nodeTypeRef</span></span> |<span data-ttu-id="59e8f-133">Узлам можно назначить разные типы узла.</span><span class="sxs-lookup"><span data-stu-id="59e8f-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="59e8f-134">Hello [типы узлов](#nodetypes) определены в разделе "hello" ниже.</span><span class="sxs-lookup"><span data-stu-id="59e8f-134">hello [node types](#nodetypes) are defined in hello section below.</span></span> |
| <span data-ttu-id="59e8f-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="59e8f-135">faultDomain</span></span> |<span data-ttu-id="59e8f-136">Ошибки домены enable Администраторы toodefine hello физических узлах кластера, может вызвать сбой во hello одновременную из-за tooshared физического зависимости.</span><span class="sxs-lookup"><span data-stu-id="59e8f-136">Fault domains enable cluster administrators toodefine hello physical nodes that might fail at hello same time due tooshared physical dependencies.</span></span> |
| <span data-ttu-id="59e8f-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="59e8f-137">upgradeDomain</span></span> |<span data-ttu-id="59e8f-138">Наборы узлов, которые будут закрыты для Service Fabric за обновляется о hello же описывают доменов обновления времени.</span><span class="sxs-lookup"><span data-stu-id="59e8f-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about hello same time.</span></span> <span data-ttu-id="59e8f-139">Можно выбрать какие узлы tooassign toowhich доменов обновления, как они не ограничивается физической требования.</span><span class="sxs-lookup"><span data-stu-id="59e8f-139">You can choose which nodes tooassign toowhich Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="59e8f-140">Свойства кластера</span><span class="sxs-lookup"><span data-stu-id="59e8f-140">Cluster properties</span></span>
<span data-ttu-id="59e8f-141">Hello **свойства** раздела hello ClusterConfig.JSON — кластер hello tooconfigure используется следующим образом.</span><span class="sxs-lookup"><span data-stu-id="59e8f-141">hello **properties** section in hello ClusterConfig.JSON is used tooconfigure hello cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="59e8f-142">Надежность</span><span class="sxs-lookup"><span data-stu-id="59e8f-142">Reliability</span></span>
<span data-ttu-id="59e8f-143">Понятие Hello **reliabilityLevel** определяет число hello реплик или экземпляры hello Service Fabric системных служб, которые могут выполняться на основных узлах hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="59e8f-143">hello concept of **reliabilityLevel** defines hello number of replicas or instances of hello Service Fabric system services that can run on hello primary nodes of hello cluster.</span></span> <span data-ttu-id="59e8f-144">Он определяет hello надежности этих служб и поэтому hello кластера.</span><span class="sxs-lookup"><span data-stu-id="59e8f-144">It determines hello reliability of these services and hence hello cluster.</span></span> <span data-ttu-id="59e8f-145">значение Hello — Вычисляемые системой hello во время создания и обновления кластера.</span><span class="sxs-lookup"><span data-stu-id="59e8f-145">hello value is calcuated by hello system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="59e8f-146">Диагностика</span><span class="sxs-lookup"><span data-stu-id="59e8f-146">Diagnostics</span></span>
<span data-ttu-id="59e8f-147">Hello **diagnosticsStore** раздел позволяет вам tooconfigure параметры tooenable диагностики и устранения неполадок узла или сбоя кластера, как показано в следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-147">hello **diagnosticsStore** section allows you tooconfigure parameters tooenable diagnostics and troubleshooting node or cluster failures, as shown in hello following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="59e8f-148">Hello **метаданные** описание диагностики кластера и может быть задано согласно настройки программы установки.</span><span class="sxs-lookup"><span data-stu-id="59e8f-148">hello **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="59e8f-149">Эти переменные помогают собирать журналы трассировки событий Windows, аварийные дампы и данные счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="59e8f-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="59e8f-150">Прочитайте статьи [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) и [Трассировка событий Windows](https://msdn.microsoft.com/library/ms751538.aspx), чтобы больше узнать о журналах трассировки событий Windows.</span><span class="sxs-lookup"><span data-stu-id="59e8f-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="59e8f-151">Все журналы, в том числе [аварийные дампы](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) и [счетчики производительности](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) может быть расширенный toohello **connectionString** папкой на компьютере.</span><span class="sxs-lookup"><span data-stu-id="59e8f-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed toohello **connectionString** folder on your machine.</span></span> <span data-ttu-id="59e8f-152">Для хранения данных диагностики можно также использовать *AzureStorage* .</span><span class="sxs-lookup"><span data-stu-id="59e8f-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="59e8f-153">Ниже приведен фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="59e8f-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="59e8f-154">Безопасность</span><span class="sxs-lookup"><span data-stu-id="59e8f-154">Security</span></span>
<span data-ttu-id="59e8f-155">Hello **безопасности** раздел необходим для безопасного автономный кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="59e8f-155">hello **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="59e8f-156">Следующий фрагмент кода Hello показана часть в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="59e8f-156">hello following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="59e8f-157">Hello **метаданные** Описание безопасного кластера и может быть задано согласно настройки программы установки.</span><span class="sxs-lookup"><span data-stu-id="59e8f-157">hello **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="59e8f-158">Hello **ClusterCredentialType** и **ServerCredentialType** определить hello тип безопасности, который будет реализовывать hello кластера и узлов hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-158">hello **ClusterCredentialType** and **ServerCredentialType** determine hello type of security that hello cluster and hello nodes will implement.</span></span> <span data-ttu-id="59e8f-159">Они могут быть заданы tooeither *X509* для обеспечения безопасности на основе сертификатов или *Windows* для обеспечения безопасности на основе Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="59e8f-159">They can be set tooeither *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="59e8f-160">Здравствуйте, остальная часть hello **безопасности** раздел будет основываться на типе hello hello безопасности.</span><span class="sxs-lookup"><span data-stu-id="59e8f-160">hello rest of hello **security** section will be based on hello type of hello security.</span></span> <span data-ttu-id="59e8f-161">Чтение [безопасности на основе сертификатов в кластере автономный](service-fabric-windows-cluster-x509-security.md) или [безопасности Windows в кластере автономный](service-fabric-windows-cluster-windows-security.md) сведения о как toofill out hello остальной части hello **безопасности**раздел.</span><span class="sxs-lookup"><span data-stu-id="59e8f-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how toofill out hello rest of hello **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="59e8f-162">Типы узлов</span><span class="sxs-lookup"><span data-stu-id="59e8f-162">Node Types</span></span>
<span data-ttu-id="59e8f-163">Hello **nodeTypes** раздел описывает тип hello hello узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="59e8f-163">hello **nodeTypes** section describes hello type of hello nodes that your cluster has.</span></span> <span data-ttu-id="59e8f-164">Необходимо указать тип хотя бы один узел в кластере, как показано в приведенном ниже фрагменте hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-164">At least one node type must be specified for a cluster, as shown in hello snippet below.</span></span> 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

<span data-ttu-id="59e8f-165">Hello **имя** hello понятное имя для этого типа узла.</span><span class="sxs-lookup"><span data-stu-id="59e8f-165">hello **name** is hello friendly name for this particular node type.</span></span> <span data-ttu-id="59e8f-166">toocreate узлом этого типа, назначить его понятное имя toohello **nodeTypeRef** переменных для этого узла, как было сказано [выше](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="59e8f-166">toocreate a node of this node type, assign its friendly name toohello **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="59e8f-167">Определения hello конечных точек подключения, которые будут использоваться для каждого типа узла.</span><span class="sxs-lookup"><span data-stu-id="59e8f-167">For each node type, define hello connection endpoints that will be used.</span></span> <span data-ttu-id="59e8f-168">Для этих конечных точек подключения можно выбрать любой номер порта, если он не конфликтует с другими конечными точками в данном кластере.</span><span class="sxs-lookup"><span data-stu-id="59e8f-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="59e8f-169">В кластер с несколькими узлами, будет один или несколько основных узла (т. е. **isPrimary** значение слишком*true*), в зависимости от hello [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="59e8f-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set too*true*), depending on hello [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="59e8f-170">Чтение [вопросы планирования емкости кластера Service Fabric](service-fabric-cluster-capacity.md) сведения о **nodeTypes** и **reliabilityLevel**и tooknow какие первичной, а hello типы узлов неосновной.</span><span class="sxs-lookup"><span data-stu-id="59e8f-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and tooknow what are primary and hello non-primary node types.</span></span> 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a><span data-ttu-id="59e8f-171">Типы узлов hello tooconfigure использовать конечные точки</span><span class="sxs-lookup"><span data-stu-id="59e8f-171">Endpoints used tooconfigure hello node types</span></span>
* <span data-ttu-id="59e8f-172">*clientConnectionEndpointPort* hello порт, используемый кластере toohello tooconnect клиента hello, при использовании интерфейсов API клиента hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-172">*clientConnectionEndpointPort* is hello port used by hello client tooconnect toohello cluster, when using hello client APIs.</span></span> 
* <span data-ttu-id="59e8f-173">*clusterConnectionEndpointPort* hello порт, по которому узлы hello взаимодействовать друг с другом.</span><span class="sxs-lookup"><span data-stu-id="59e8f-173">*clusterConnectionEndpointPort* is hello port at which hello nodes communicate with each other.</span></span>
* <span data-ttu-id="59e8f-174">*leaseDriverEndpointPort* hello порт, используемый с hello кластера аренды драйвер toofind out, если узлы hello все еще активны.</span><span class="sxs-lookup"><span data-stu-id="59e8f-174">*leaseDriverEndpointPort* is hello port used by hello cluster lease driver toofind out if hello nodes are still active.</span></span> 
* <span data-ttu-id="59e8f-175">*serviceConnectionEndpointPort* hello порт, используемый hello приложений и служб, развернутых на узле, toocommunicate с клиентом hello Service Fabric на данном узле.</span><span class="sxs-lookup"><span data-stu-id="59e8f-175">*serviceConnectionEndpointPort* is hello port used by hello applications and services deployed on a node, toocommunicate with hello Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="59e8f-176">*httpGatewayEndpointPort* hello порт, используемый кластером toohello tooconnect Service Fabric Explorer hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-176">*httpGatewayEndpointPort* is hello port used by hello Service Fabric Explorer tooconnect toohello cluster.</span></span>
* <span data-ttu-id="59e8f-177">*ephemeralPorts* переопределить hello [динамические порты, используемые hello ОС](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="59e8f-177">*ephemeralPorts* override hello [dynamic ports used by hello OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="59e8f-178">Service Fabric будет использовать часть эти порты приложения и оставшихся hello будут доступны для hello ОС.</span><span class="sxs-lookup"><span data-stu-id="59e8f-178">Service Fabric will use a part of these as application ports and hello remaining will be available for hello OS.</span></span> <span data-ttu-id="59e8f-179">Его также потребуется сопоставить этот диапазон toohello существующего диапазона в hello ОС, для любых целей при выборе hello диапазоны для данных в файлах JSON образец hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-179">It will also map this range toohello existing range present in hello OS, so for all purposes, you can use hello ranges given in hello sample JSON files.</span></span> <span data-ttu-id="59e8f-180">Необходимо удостовериться, что hello разницу между началом hello и серверных портов hello имеет по крайней мере 255 toomake.</span><span class="sxs-lookup"><span data-stu-id="59e8f-180">You need toomake sure that hello difference between hello start and hello end ports is at least 255.</span></span> <span data-ttu-id="59e8f-181">Возможно возникновение конфликтов, если это различие слишком мал, так как этот диапазон используется совместно с hello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="59e8f-181">You may run into conflicts if this difference is too low, since this range is shared with hello operating system.</span></span> <span data-ttu-id="59e8f-182">В разделе hello настроен динамический диапазон портов запустив `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="59e8f-182">See hello configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="59e8f-183">*applicationPorts* hello портов, которые будут использоваться приложениями Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-183">*applicationPorts* are hello ports that will be used by hello Service Fabric applications.</span></span> <span data-ttu-id="59e8f-184">диапазон портов приложения Hello должно быть достаточно большим, toocover hello конечной точки требования приложений.</span><span class="sxs-lookup"><span data-stu-id="59e8f-184">hello application port range should be large enough toocover hello endpoint requirement of your applications.</span></span> <span data-ttu-id="59e8f-185">Этот диапазон должен быть со hello динамический диапазон портов на компьютере hello, т. е. hello *ephemeralPorts* диапазона, как указано в конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-185">This range should be exclusive from hello dynamic port range on hello machine, i.e. hello *ephemeralPorts* range as set in hello configuration.</span></span>  <span data-ttu-id="59e8f-186">Service Fabric будут использовать каждый раз, когда новые порты являются обязательными, а также Будьте внимательны открыть брандмауэр Windows hello для этих портов.</span><span class="sxs-lookup"><span data-stu-id="59e8f-186">Service Fabric will use these whenever new ports are required, as well as take care of opening hello firewall for these ports.</span></span> 
* <span data-ttu-id="59e8f-187">*reverseProxyEndpointPort* — это необязательная конечная точка обратного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="59e8f-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="59e8f-188">Дополнительные сведения см. в статье [Обратный прокси-сервер Service Fabric](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="59e8f-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="59e8f-189">Параметры журнала</span><span class="sxs-lookup"><span data-stu-id="59e8f-189">Log Settings</span></span>
<span data-ttu-id="59e8f-190">Hello **fabricSettings** раздел позволяет вам tooset hello корневые каталоги для hello Service Fabric данных и журналов.</span><span class="sxs-lookup"><span data-stu-id="59e8f-190">hello **fabricSettings** section allows you tooset hello root directories for hello Service Fabric data and logs.</span></span> <span data-ttu-id="59e8f-191">Можно изменить только во время создания исходного кластера hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-191">You can customize these only during hello initial cluster creation.</span></span> <span data-ttu-id="59e8f-192">Ниже приведен фрагмент кода из этого раздела.</span><span class="sxs-lookup"><span data-stu-id="59e8f-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="59e8f-193">Рекомендуется использование диска без ОС в качестве hello FabricDataRoot и FabricLogRoot, как она обеспечивает большую надежность от взломов ОС.</span><span class="sxs-lookup"><span data-stu-id="59e8f-193">We recommended using a non-OS drive as hello FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="59e8f-194">Обратите внимание, что при настройке только корневой каталог данных hello затем hello журнала корневой помещаются на один уровень ниже корневой каталог данных hello.</span><span class="sxs-lookup"><span data-stu-id="59e8f-194">Note that if you customize only hello data root, then hello log root will be placed one level below hello data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="59e8f-195">Параметры надежной службы с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="59e8f-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="59e8f-196">Hello **KtlLogger** раздел позволяет вам tooset hello глобальные параметры конфигурации для надежного обмена.</span><span class="sxs-lookup"><span data-stu-id="59e8f-196">hello **KtlLogger** section allows you tooset hello global configuration settings for Reliable Services.</span></span> <span data-ttu-id="59e8f-197">Дополнительные сведения об этих параметрах см. в разделе [Настройка надежных служб с отслеживанием состояния](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="59e8f-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="59e8f-198">Hello приведенном ниже примере показаны toochange hello hello общего журнала транзакций, которая возвращает созданные tooback коллекций надежных служб с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="59e8f-198">hello example below shows how toochange hello hello shared transaction log that gets created tooback any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="59e8f-199">Функции надстройки</span><span class="sxs-lookup"><span data-stu-id="59e8f-199">Add-on features</span></span>
<span data-ttu-id="59e8f-200">tooconfigure дополнительных функций, hello apiVersion должен, настроенных как "04-2017' или более поздней версии и addonFeatures должен настроить toobe:</span><span class="sxs-lookup"><span data-stu-id="59e8f-200">tooconfigure add-on features, hello apiVersion should be configured as '04-2017' or higher, and addonFeatures needs toobe configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="59e8f-201">Поддержка контейнеров</span><span class="sxs-lookup"><span data-stu-id="59e8f-201">Container support</span></span>
<span data-ttu-id="59e8f-202">Поддержка tooenable контейнера для контейнеров windows server и контейнеров hyper-v для изолированные кластеры, компонент надстройки «DnsService» hello должен toobe включена.</span><span class="sxs-lookup"><span data-stu-id="59e8f-202">tooenable container support for both windows server container and hyper-v container for standalone clusters, hello 'DnsService' add-on feature needs toobe enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="59e8f-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59e8f-203">Next steps</span></span>
<span data-ttu-id="59e8f-204">После завершения файла ClusterConfig.JSON настроен в соответствии с вашей установки кластера, можно развернуть кластер в следующей статье hello [создание кластера Service Fabric автономный](service-fabric-cluster-creation-for-windows-server.md) и затем продолжить слишком[визуализация кластера с Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="59e8f-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following hello article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed too[visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

