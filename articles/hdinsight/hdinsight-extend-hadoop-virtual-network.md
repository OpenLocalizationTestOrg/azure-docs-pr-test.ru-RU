---
title: "aaaExtend HDInsight с помощью виртуальной сети - Azure | Документы Microsoft"
description: "Дополнительные сведения об toouse виртуальной сети Azure tooconnect HDInsight tooother облачных ресурсов, или в центре обработки данных"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="c7e8f-103">Расширение возможностей HDInsight с помощью виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="c7e8f-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="c7e8f-104">Узнайте, как toouse HDInsight с [виртуальной сети Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7e8f-104">Learn how toouse HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="c7e8f-105">С помощью виртуальной сети Azure обеспечивает hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-105">Using an Azure Virtual Network enables hello following scenarios:</span></span>

* <span data-ttu-id="c7e8f-106">Подключение tooHDInsight непосредственно из локальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-106">Connecting tooHDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="c7e8f-107">Подключение HDInsight toodata хранятся в Azure в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-107">Connecting HDInsight toodata stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="c7e8f-108">Непосредственно доступ к службам Hadoop, которые недоступны в более публично hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-108">Directly accessing Hadoop services that are not available publicly over hello internet.</span></span> <span data-ttu-id="c7e8f-109">Например API-интерфейсов Kafka или hello HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-109">For example, Kafka APIs or hello HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="c7e8f-110">в этом документе сведения Hello требует понимания сети TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-110">hello information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="c7e8f-111">Если вы не знакомы с конфигурацией сети TCP/IP, следует сотрудничества с пользователями, прежде чем вносить изменения tooproduction сетей.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications tooproduction networks.</span></span>

## <a name="planning"></a><span data-ttu-id="c7e8f-112">Планирование</span><span class="sxs-lookup"><span data-stu-id="c7e8f-112">Planning</span></span>

<span data-ttu-id="c7e8f-113">Здесь представлены Hello hello вопросы, которые должен ответить при планировании tooinstall HDInsight в виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-113">hello following are hello questions that you must answer when planning tooinstall HDInsight in a virtual network:</span></span>

* <span data-ttu-id="c7e8f-114">Требуется tooinstall HDInsight в существующей виртуальной сети?</span><span class="sxs-lookup"><span data-stu-id="c7e8f-114">Do you need tooinstall HDInsight into an existing virtual network?</span></span> <span data-ttu-id="c7e8f-115">Или вы создаете новую сеть?</span><span class="sxs-lookup"><span data-stu-id="c7e8f-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="c7e8f-116">При использовании существующей виртуальной сети, может потребоваться toomodify hello сетевой конфигурации перед установкой HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-116">If you are using an existing virtual network, you may need toomodify hello network configuration before you can install HDInsight.</span></span> <span data-ttu-id="c7e8f-117">Дополнительные сведения см. в разделе hello [добавить виртуальную сеть с существующие HDInsight tooan](#existingvnet) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-117">For more information, see hello [add HDInsight tooan existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="c7e8f-118">Вы хотите tooconnect hello виртуальная сеть, содержащая HDInsight tooanother виртуальной сети или в локальной сети?</span><span class="sxs-lookup"><span data-stu-id="c7e8f-118">Do you want tooconnect hello virtual network containing HDInsight tooanother virtual network or your on-premises network?</span></span>

    <span data-ttu-id="c7e8f-119">tooeasily работы с ресурсами в сетях может требуется toocreate пользовательские DNS и настройте DNS.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-119">tooeasily work with resources across networks, you may need toocreate a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="c7e8f-120">Дополнительные сведения см. в разделе hello [подключение нескольких сетей](#multinet) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-120">For more information, see hello [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="c7e8f-121">Вы хотите toorestrict перенаправление tooHDInsight входящего и исходящего трафика?</span><span class="sxs-lookup"><span data-stu-id="c7e8f-121">Do you want toorestrict/redirect inbound or outbound traffic tooHDInsight?</span></span>

    <span data-ttu-id="c7e8f-122">HDInsight необходимо имеют неограниченный связь с определенных IP-адресов в центре обработки данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-122">HDInsight must have unrestricted communication with specific IP addresses in hello Azure data center.</span></span> <span data-ttu-id="c7e8f-123">Существует несколько портов, которые следует разрешить в брандмауэрах для взаимодействия с клиентами.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="c7e8f-124">Дополнительные сведения см. в разделе hello [управлению сетевым трафиком](#networktraffic) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-124">For more information, see hello [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="c7e8f-125"><a id="existingvnet"></a>Добавить HDInsight tooan существующей виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="c7e8f-125"><a id="existingvnet"></a>Add HDInsight tooan existing virtual network</span></span>

<span data-ttu-id="c7e8f-126">Как использовать действия hello в этот раздел toodiscover tooadd новый tooan HDInsight с существующей виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-126">Use hello steps in this section toodiscover how tooadd a new HDInsight tooan existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="c7e8f-127">В виртуальную сеть невозможно добавить существующий кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="c7e8f-128">Используется классический или модели развертывания диспетчера ресурсов для hello виртуальной сети?</span><span class="sxs-lookup"><span data-stu-id="c7e8f-128">Are you using a classic or Resource Manager deployment model for hello virtual network?</span></span>

    <span data-ttu-id="c7e8f-129">Для HDInsight 3.4 и более поздней версии требуется виртуальная сеть диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="c7e8f-130">Для работы более ранних версий HDInsight требовалась классическая виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="c7e8f-131">При наличии существующей сети классической виртуальной сети, необходимо создать виртуальную сеть диспетчера ресурсов и подключитесь hello два.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect hello two.</span></span> <span data-ttu-id="c7e8f-132">[Подключение классических виртуальных сетей toonew виртуальных сетей](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c7e8f-132">[Connecting classic VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="c7e8f-133">После присоединения, HDInsight установлен в диспетчер ресурсов сети hello могут взаимодействовать с ресурсы в сети классический hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-133">Once joined, HDInsight installed in hello Resource Manager network can interact with resources in hello classic network.</span></span>

2. <span data-ttu-id="c7e8f-134">Используется ли принудительное туннелирование?</span><span class="sxs-lookup"><span data-stu-id="c7e8f-134">Do you use forced tunneling?</span></span> <span data-ttu-id="c7e8f-135">Принудительное туннелирование — подсеть, требующем исходящего Интернет трафика tooa устройства для проверки и ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-135">Forced tunneling is a subnet setting that forces outbound Internet traffic tooa device for inspection and logging.</span></span> <span data-ttu-id="c7e8f-136">HDInsight не поддерживает принудительное туннелирование.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="c7e8f-137">Перед установкой HDInsight в подсеть либо удалите принудительное туннелирование, либо создайте новую подсеть для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="c7e8f-138">Нужны Сетевые группы безопасности, определяемых пользователем маршрутов или виртуальные сетевые устройства toorestrict трафика в или из hello виртуальной сети?</span><span class="sxs-lookup"><span data-stu-id="c7e8f-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances toorestrict traffic into or out of hello virtual network?</span></span>

    <span data-ttu-id="c7e8f-139">В качестве управляемой службы HDInsight требуется неограниченный доступ tooseveral IP-адресов в центре обработки данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-139">As a managed service, HDInsight requires unrestricted access tooseveral IP addresses in hello Azure data center.</span></span> <span data-ttu-id="c7e8f-140">связь tooallow с этих IP-адресов, обновить существующие группы безопасности сети и определяемых пользователем маршрутов.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-140">tooallow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="c7e8f-141">В состав HDInsight входит несколько служб, которые используют различные порты.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="c7e8f-142">Не блокируют трафик toothese портов.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-142">Do not block traffic toothese ports.</span></span> <span data-ttu-id="c7e8f-143">Список портов tooallow брандмауэрах виртуальных устройств см. в разделе hello [безопасности](#security) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-143">For a list of ports tooallow through virtual appliance firewalls, see hello [Security](#security) section.</span></span>

    <span data-ttu-id="c7e8f-144">toofind существующей конфигурации безопасности, hello используйте следующие команды Azure PowerShell или Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-144">toofind your existing security configuration, use hello following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="c7e8f-145">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="c7e8f-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="c7e8f-146">Дополнительные сведения см. в разделе hello [Устранение сетевых групп безопасности](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-146">For more information, see hello [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="c7e8f-147">Правила группы безопасности сети применяются в порядке, основанном на приоритете правила.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="c7e8f-148">применяется первое правило Hello, соответствующую шаблону трафика hello и другие применяются для этого трафика.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-148">hello first rule that matches hello traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="c7e8f-149">Порядок правила с максимальными tooleast разрешительным.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-149">Order rules from most permissive tooleast permissive.</span></span> <span data-ttu-id="c7e8f-150">Дополнительные сведения см. в разделе hello [фильтрации трафика с группами безопасности сети](../virtual-network/virtual-networks-nsg.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-150">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="c7e8f-151">Определяемые пользователем маршруты</span><span class="sxs-lookup"><span data-stu-id="c7e8f-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="c7e8f-152">Дополнительные сведения см. в разделе hello [Устранение маршруты](../virtual-network/virtual-network-routes-troubleshoot-portal.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-152">For more information, see hello [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="c7e8f-153">Создание кластера HDInsight и выбора hello виртуальной сети Azure во время установки.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-153">Create an HDInsight cluster and select hello Azure Virtual Network during configuration.</span></span> <span data-ttu-id="c7e8f-154">Выполните шаги hello в следующих toounderstand документы в процессе создания кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-154">Use hello steps in hello following documents toounderstand hello cluster creation process:</span></span>

    * [<span data-ttu-id="c7e8f-155">Создание с помощью hello портал Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7e8f-155">Create HDInsight using hello Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="c7e8f-156">Создание кластера HDInsight с использованием Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7e8f-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="c7e8f-157">Создание кластеров HDInsight с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="c7e8f-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="c7e8f-158">Создание кластеров Hadoop в HDInsight с помощью шаблонов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7e8f-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="c7e8f-159">Добавление HDInsight tooa виртуальной сети — это шаг дополнительная настройка.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-159">Adding HDInsight tooa virtual network is an optional configuration step.</span></span> <span data-ttu-id="c7e8f-160">При настройке кластера hello, быть виртуальной сети, что tooselect hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-160">Be sure tooselect hello virtual network when configuring hello cluster.</span></span>

## <span data-ttu-id="c7e8f-161"><a id="multinet"></a>Подключение нескольких сетей</span><span class="sxs-lookup"><span data-stu-id="c7e8f-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="c7e8f-162">сложная задача Hello с несколькими сетевая конфигурация является разрешение имен между сетями hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-162">hello biggest challenge with a multi-network configuration is name resolution between hello networks.</span></span>

<span data-ttu-id="c7e8f-163">Azure предоставляет разрешение имен для служб Azure, установленных в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="c7e8f-164">Это разрешение встроенным именем позволяет toohello tooconnect HDInsight следующие ресурсы с помощью полного доменного имени (FQDN):</span><span class="sxs-lookup"><span data-stu-id="c7e8f-164">This built-in name resolution allows HDInsight tooconnect toohello following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="c7e8f-165">Любой ресурс, доступный на hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-165">Any resource that is available on hello internet.</span></span> <span data-ttu-id="c7e8f-166">например, microsoft.com, google.com;</span><span class="sxs-lookup"><span data-stu-id="c7e8f-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="c7e8f-167">Любые ресурсы, в hello одной виртуальной сети Azure с помощью hello __внутренние имена DNS__ hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-167">Any resource that is in hello same Azure Virtual Network, by using hello __internal DNS name__ of hello resource.</span></span> <span data-ttu-id="c7e8f-168">Например при использовании разрешение имен по умолчанию hello, hello представлены пример внутренней DNS имена назначенного tooHDInsight рабочих узлов:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-168">For example, when using hello default name resolution, hello following are example internal DNS names assigned tooHDInsight worker nodes:</span></span>

    * <span data-ttu-id="c7e8f-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net;</span><span class="sxs-lookup"><span data-stu-id="c7e8f-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="c7e8f-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="c7e8f-171">Оба этих узла могут взаимодействовать напрямую друг с другом и с другими узлами в HDInsight, используя внутренние DNS-имена.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="c7e8f-172">разрешение имен по умолчанию Hello __не__ разрешить HDInsight tooresolve hello имена ресурсов в сетях, которые будут присоединены к домену toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-172">hello default name resolution does __not__ allow HDInsight tooresolve hello names of resources in networks that are joined toohello virtual network.</span></span> <span data-ttu-id="c7e8f-173">Например, это общие toojoin в локальной сети toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-173">For example, it is common toojoin your on-premises network toohello virtual network.</span></span> <span data-ttu-id="c7e8f-174">Только hello разрешения имени по умолчанию HDInsight не может обращаться к ресурсам локальной сети hello по имени.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-174">With only hello default name resolution, HDInsight cannot access resources in hello on-premises network by name.</span></span> <span data-ttu-id="c7e8f-175">Hello противоположной также имеет значение true, ресурсам в локальной сети не доступ к ресурсам в виртуальной сети hello по имени.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-175">hello opposite is also true, resources in your on-premises network cannot access resources in hello virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="c7e8f-176">Необходимо создать hello пользовательского DNS-сервера и настроить виртуальную сеть toouse hello его перед созданием hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-176">You must create hello custom DNS server and configure hello virtual network toouse it before creating hello HDInsight cluster.</span></span>

<span data-ttu-id="c7e8f-177">tooenable разрешение имен между hello виртуальной сети и ресурсами в сетях, присоединены к домену, необходимо выполнить hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-177">tooenable name resolution between hello virtual network and resources in joined networks, you must perform hello following actions:</span></span>

1. <span data-ttu-id="c7e8f-178">Создание пользовательского DNS-сервера в виртуальной сети Azure, где планируется tooinstall HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-178">Create a custom DNS server in hello Azure Virtual Network where you plan tooinstall HDInsight.</span></span>

2. <span data-ttu-id="c7e8f-179">Настройте hello виртуальной сети toouse hello пользовательского DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-179">Configure hello virtual network toouse hello custom DNS server.</span></span>

3. <span data-ttu-id="c7e8f-180">Найти hello Azure назначать DNS-суффикса для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-180">Find hello Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="c7e8f-181">Это значение аналогично слишком`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-181">This value is similar too`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="c7e8f-182">Сведения о поиске hello DNS-суффикс в разделе hello [пример: Настройка DNS](#example-dns) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-182">For information on finding hello DNS suffix, see hello [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="c7e8f-183">Настройка перенаправления между hello DNS-серверов.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-183">Configure forwarding between hello DNS servers.</span></span> <span data-ttu-id="c7e8f-184">Конфигурация Hello зависит от типа hello удаленной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-184">hello configuration depends on hello type of remote network.</span></span>

    * <span data-ttu-id="c7e8f-185">Если hello удаленной сети к локальной сети, настройте DNS следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-185">If hello remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="c7e8f-186">__Пользовательские DNS__ (в виртуальной сети hello):</span><span class="sxs-lookup"><span data-stu-id="c7e8f-186">__Custom DNS__ (in hello virtual network):</span></span>

            * <span data-ttu-id="c7e8f-187">Перенаправлять запросы DNS-суффикс hello hello виртуальной сети toohello Azure рекурсивного сопоставителя (168.63.129.16).</span><span class="sxs-lookup"><span data-stu-id="c7e8f-187">Forward requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="c7e8f-188">Azure обрабатывает запросы к ресурсам в виртуальной сети hello</span><span class="sxs-lookup"><span data-stu-id="c7e8f-188">Azure handles requests for resources in hello virtual network</span></span>

            * <span data-ttu-id="c7e8f-189">Пересылка всех других запросов toohello локального DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-189">Forward all other requests toohello on-premises DNS server.</span></span> <span data-ttu-id="c7e8f-190">Hello на локальном DNS обрабатывает все остальные запросы на разрешение имен, включая запросы для Интернет-ресурсов как Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-190">hello on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="c7e8f-191">__Локальный DNS__: перенаправление запросов для hello виртуальной сети DNS-суффикс toohello пользовательские DNS сервера.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-191">__On-premises DNS__: Forward requests for hello virtual network DNS suffix toohello custom DNS server.</span></span> <span data-ttu-id="c7e8f-192">Hello пользовательские DNS-сервер переадресует toohello Azure рекурсивного сопоставителя.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-192">hello custom DNS server then forwards toohello Azure recursive resolver.</span></span>

        <span data-ttu-id="c7e8f-193">Запросы маршруты этой конфигурации для полные доменные имена, которые содержат hello DNS-суффикс hello виртуальной сети toohello пользовательского DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-193">This configuration routes requests for fully qualified domain names that contain hello DNS suffix of hello virtual network toohello custom DNS server.</span></span> <span data-ttu-id="c7e8f-194">Все запросы (даже для общедоступных адресов Интернета) обрабатываются hello локального DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-194">All other requests (even for public internet addresses) are handled by hello on-premises DNS server.</span></span>

    * <span data-ttu-id="c7e8f-195">Если другой виртуальной сети Azure hello удаленной сети, настройте DNS следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-195">If hello remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="c7e8f-196">__Пользовательский DNS-сервер__ (в каждой виртуальной сети):</span><span class="sxs-lookup"><span data-stu-id="c7e8f-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="c7e8f-197">Запросы DNS-суффикс hello hello виртуальных сетей, перенаправляются toohello пользовательские DNS-серверы.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-197">Requests for hello DNS suffix of hello virtual networks are forwarded toohello custom DNS servers.</span></span> <span data-ttu-id="c7e8f-198">для разрешения ресурсов в пределах своей сети отвечает Hello DNS в каждой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-198">hello DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="c7e8f-199">Пересылка всех других запросов toohello Azure рекурсивного сопоставителя.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-199">Forward all other requests toohello Azure recursive resolver.</span></span> <span data-ttu-id="c7e8f-200">Hello рекурсивного сопоставителя отвечает за разрешает локальные и Интернет-ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-200">hello recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="c7e8f-201">Hello DNS-сервер для каждой сети перенаправляет запросы toohello другим, основываясь на DNS-суффикс.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-201">hello DNS server for each network forwards requests toohello other, based on DNS suffix.</span></span> <span data-ttu-id="c7e8f-202">Другие запросы разрешаются с помощью hello Azure рекурсивного сопоставителя.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-202">Other requests are resolved using hello Azure recursive resolver.</span></span>

    <span data-ttu-id="c7e8f-203">Пример каждой конфигурации см. в разделе hello [пример: Настройка DNS](#example-dns) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-203">For an example of each configuration, see hello [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="c7e8f-204">Дополнительные сведения см. в разделе hello [разрешение имен для виртуальных машин и экземпляров ролей](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-204">For more information, see hello [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-toohadoop-services"></a><span data-ttu-id="c7e8f-205">Подключение непосредственно tooHadoop служб</span><span class="sxs-lookup"><span data-stu-id="c7e8f-205">Directly connect tooHadoop services</span></span>

<span data-ttu-id="c7e8f-206">Большая часть документации по HDInsight предполагается, что кластер toohello доступ через hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-206">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="c7e8f-207">Например, возможность подключения кластера toohello в https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-207">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="c7e8f-208">Этот адрес используется hello открытый шлюз, который недоступен, если вы использовали Nsg или Здравствуйте, UDRs toorestrict доступ из Интернета.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-208">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="c7e8f-209">tooconnect tooAmbari и других веб-страницы через hello виртуальную сеть, использовать hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-209">tooconnect tooAmbari and other web pages through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="c7e8f-210">hello toodiscover внутренней полные доменные имена (FQDN) узлов кластера HDInsight hello, используйте один из hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-210">toodiscover hello internal fully qualified domain names (FQDN) of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    <span data-ttu-id="c7e8f-211">В список узлов, возвращаемых hello найти hello полное доменное имя для hello головного узла и используйте tooAmbari tooconnect hello полных доменных имен и других веб-служб.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-211">In hello list of nodes returned, find hello FQDN for hello head nodes and use hello FQDNs tooconnect tooAmbari and other web services.</span></span> <span data-ttu-id="c7e8f-212">Например, использовать `http://<headnode-fqdn>:8080` tooaccess Ambari.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-212">For example, use `http://<headnode-fqdn>:8080` tooaccess Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c7e8f-213">Некоторые службы, размещенной на hello головного узла активны только на одном узле одновременно.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-213">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="c7e8f-214">При попытке доступа к службе на один головной узел и его возвращает ошибку 404, переключение toohello других головного узла.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-214">If you try accessing a service on one head node and it returns a 404 error, switch toohello other head node.</span></span>

2. <span data-ttu-id="c7e8f-215">toodetermine hello узел и порт, который доступен на, см. раздел hello [порты, используемые службами Hadoop в HDInsight](./hdinsight-hadoop-port-settings-for-services.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-215">toodetermine hello node and port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="c7e8f-216"><a id="networktraffic"></a>Управление сетевым трафиком</span><span class="sxs-lookup"><span data-stu-id="c7e8f-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="c7e8f-217">Сетевой трафик в виртуальные сети Azure можно управлять с помощью hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-217">Network traffic in an Azure Virtual Networks can be controlled using hello following methods:</span></span>

* <span data-ttu-id="c7e8f-218">**Сетевых групп безопасности** (NSG) позволяют сети toohello toofilter входящего и исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-218">**Network security groups** (NSG) allow you toofilter inbound and outbound traffic toohello network.</span></span> <span data-ttu-id="c7e8f-219">Дополнительные сведения см. в разделе hello [фильтрации трафика с группами безопасности сети](../virtual-network/virtual-networks-nsg.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-219">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="c7e8f-220">HDInsight не поддерживает ограничение исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="c7e8f-221">**Определяемые пользователем маршруты** (UDR) определяют, как проходит трафик между ресурсами в сети hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-221">**User-defined routes** (UDR) define how traffic flows between resources in hello network.</span></span> <span data-ttu-id="c7e8f-222">Дополнительные сведения см. в разделе hello [определяемые пользователем маршруты и IP-пересылки](../virtual-network/virtual-networks-udr-overview.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-222">For more information, see hello [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="c7e8f-223">**Сети виртуальных приборов** реплицировать hello функциональные возможности устройства, например брандмауэров и маршрутизаторов.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-223">**Network virtual appliances** replicate hello functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="c7e8f-224">Дополнительные сведения см. в разделе hello [сетевые устройства](https://azure.microsoft.com/solutions/network-appliances) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-224">For more information, see hello [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="c7e8f-225">Как управляемая служба HDInsight требуется неограниченный доступ tooAzure работоспособности и управлять ими в облаке Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-225">As a managed service, HDInsight requires unrestricted access tooAzure health and management services in hello Azure cloud.</span></span> <span data-ttu-id="c7e8f-226">При использовании NSG и UDR необходимо убедиться, что эти службы могут взаимодействовать с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="c7e8f-227">HDInsight предоставляет службы на нескольких портах.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="c7e8f-228">При использовании брандмауэра виртуальное устройство, необходимо разрешить трафик через hello порты, используемые для этих служб.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-228">When using a virtual appliance firewall, you must allow traffic on hello ports used for these services.</span></span> <span data-ttu-id="c7e8f-229">Дополнительные сведения см в разделе [требуемые порты] hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-229">For more information, see hello [Required ports] section.</span></span>

### <span data-ttu-id="c7e8f-230"><a id="hdinsight-ip"></a>HDInsight с группами безопасности сети и определяемые пользователем маршрутами</span><span class="sxs-lookup"><span data-stu-id="c7e8f-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="c7e8f-231">Если вы планируете использовать **сетевых групп безопасности** или **определяемых пользователем маршрутов** toocontrol сетевого трафика, выполните следующие действия перед установкой HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-231">If you plan on using **network security groups** or **user-defined routes** toocontrol network traffic, perform hello following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="c7e8f-232">Определите hello регион Azure, планирование toouse HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-232">Identify hello Azure region that you plan toouse for HDInsight.</span></span>

2. <span data-ttu-id="c7e8f-233">Определите hello IP-адреса, необходимые для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-233">Identify hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="c7e8f-234">Дополнительные сведения см. в разделе hello [IP-адреса, необходимые для HDInsight](#hdinsight-ip) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-234">For more information, see hello [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="c7e8f-235">Создание или изменение группы безопасности сети hello или определяемых пользователем маршрутов для подсети hello планировать tooinstall HDInsight в.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-235">Create or modify hello network security groups or user-defined routes for hello subnet that you plan tooinstall HDInsight into.</span></span>

    * <span data-ttu-id="c7e8f-236">__Сетевых групп безопасности__: Разрешить __входящий__ трафик через порт __443__ с hello IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-236">__Network security groups__: allow __inbound__ traffic on port __443__ from hello IP addresses.</span></span>
    * <span data-ttu-id="c7e8f-237">__Определяемые пользователем маршруты__: создание IP-адрес маршрута tooeach и задание hello __тип следующего прыжка__ too__Internet__.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-237">__User-defined routes__: create a route tooeach IP address and set hello __Next hop type__ too__Internet__.</span></span>

<span data-ttu-id="c7e8f-238">Дополнительные сведения о сетевых групп безопасности и определяемых пользователем маршрутов см. следующие документации hello:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-238">For more information on network security groups or user-defined routes, see hello following documentation:</span></span>

* <span data-ttu-id="c7e8f-239">[группа безопасности сети](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="c7e8f-239">[Network security group](../virtual-network/virtual-networks-nsg.md)</span></span>

* [<span data-ttu-id="c7e8f-240">Определяемые пользователем маршруты</span><span class="sxs-lookup"><span data-stu-id="c7e8f-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="c7e8f-241">Принудительное туннелирование</span><span class="sxs-lookup"><span data-stu-id="c7e8f-241">Forced tunneling</span></span>

<span data-ttu-id="c7e8f-242">Принудительное туннелирование это определяемая пользователем конфигурация маршрутизации, где весь трафик из подсети принудительное tooa определенным сети или в расположении, например в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced tooa specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="c7e8f-243">HDInsight __не__поддерживает принудительное туннелирование.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="c7e8f-244"><a id="hdinsight-ip"></a> Требуемые IP-адреса</span><span class="sxs-lookup"><span data-stu-id="c7e8f-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7e8f-245">Hello Azure работоспособности и службы управления должен быть доступ toocommunicate с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-245">hello Azure health and management services must be able toocommunicate with HDInsight.</span></span> <span data-ttu-id="c7e8f-246">Если вы используете группы безопасности сети и определяемых пользователем маршрутов, разрешите трафик от hello IP-адресов для этих служб tooreach HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-246">If you use network security groups or user-defined routes, allow traffic from hello IP addresses for these services tooreach HDInsight.</span></span>
>
> <span data-ttu-id="c7e8f-247">Если не используется группами безопасности сети или трафик toocontrol определяемых пользователем маршрутов, можно игнорировать в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-247">If you do not use network security groups or user-defined routes toocontrol traffic, you can ignore this section.</span></span>

<span data-ttu-id="c7e8f-248">При использовании групп безопасности сети и определяемых пользователем маршрутов, необходимо разрешить трафик от hello Azure health и tooreach управления службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-248">If you use network security groups or user-defined routes, you must allow traffic from hello Azure health and management services tooreach HDInsight.</span></span> <span data-ttu-id="c7e8f-249">Используйте следующие hello действия toofind hello IP-адресов, которые должны быть разрешены.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-249">Use hello following steps toofind hello IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="c7e8f-250">Всегда необходимо разрешить трафик от hello следующие IP-адреса:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-250">You must always allow traffic from hello following IP addresses:</span></span>

    | <span data-ttu-id="c7e8f-251">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="c7e8f-251">IP address</span></span> | <span data-ttu-id="c7e8f-252">Разрешенный порт</span><span class="sxs-lookup"><span data-stu-id="c7e8f-252">Allowed port</span></span> | <span data-ttu-id="c7e8f-253">Направление</span><span class="sxs-lookup"><span data-stu-id="c7e8f-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="c7e8f-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="c7e8f-254">168.61.49.99</span></span> | <span data-ttu-id="c7e8f-255">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-255">443</span></span> | <span data-ttu-id="c7e8f-256">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-256">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="c7e8f-257">23.99.5.239</span></span> | <span data-ttu-id="c7e8f-258">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-258">443</span></span> | <span data-ttu-id="c7e8f-259">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-259">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="c7e8f-260">168.61.48.131</span></span> | <span data-ttu-id="c7e8f-261">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-261">443</span></span> | <span data-ttu-id="c7e8f-262">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-262">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="c7e8f-263">138.91.141.162</span></span> | <span data-ttu-id="c7e8f-264">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-264">443</span></span> | <span data-ttu-id="c7e8f-265">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-265">Inbound</span></span> |

2. <span data-ttu-id="c7e8f-266">Если ваш HDInsight кластер находится в одном из следующих областей hello, необходимо разрешить трафик от hello IP-адресов для области hello:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-266">If your HDInsight cluster is in one of hello following regions, then you must allow traffic from hello IP addresses listed for hello region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c7e8f-267">Если регион Azure, которую вы используете hello не указан, то используйте только hello четыре IP-адреса из шага 1.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-267">If hello Azure region you are using is not listed, then only use hello four IP addresses from step 1.</span></span>

    | <span data-ttu-id="c7e8f-268">Страна</span><span class="sxs-lookup"><span data-stu-id="c7e8f-268">Country</span></span> | <span data-ttu-id="c7e8f-269">Регион</span><span class="sxs-lookup"><span data-stu-id="c7e8f-269">Region</span></span> | <span data-ttu-id="c7e8f-270">Разрешенные IP-адреса</span><span class="sxs-lookup"><span data-stu-id="c7e8f-270">Allowed IP addresses</span></span> | <span data-ttu-id="c7e8f-271">Разрешенный порт</span><span class="sxs-lookup"><span data-stu-id="c7e8f-271">Allowed port</span></span> | <span data-ttu-id="c7e8f-272">Направление</span><span class="sxs-lookup"><span data-stu-id="c7e8f-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="c7e8f-273">Азия</span><span class="sxs-lookup"><span data-stu-id="c7e8f-273">Asia</span></span> | <span data-ttu-id="c7e8f-274">Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="c7e8f-274">East Asia</span></span> | <span data-ttu-id="c7e8f-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="c7e8f-275">23.102.235.122</span></span></br><span data-ttu-id="c7e8f-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="c7e8f-276">52.175.38.134</span></span> | <span data-ttu-id="c7e8f-277">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-277">443</span></span> | <span data-ttu-id="c7e8f-278">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-279">Юго-Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="c7e8f-279">Southeast Asia</span></span> | <span data-ttu-id="c7e8f-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="c7e8f-280">13.76.245.160</span></span></br><span data-ttu-id="c7e8f-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="c7e8f-281">13.76.136.249</span></span> | <span data-ttu-id="c7e8f-282">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-282">443</span></span> | <span data-ttu-id="c7e8f-283">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-283">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-284">Австралия</span><span class="sxs-lookup"><span data-stu-id="c7e8f-284">Australia</span></span> | <span data-ttu-id="c7e8f-285">Восточная часть Австралии</span><span class="sxs-lookup"><span data-stu-id="c7e8f-285">Australia East</span></span> | <span data-ttu-id="c7e8f-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="c7e8f-286">104.210.84.115</span></span></br><span data-ttu-id="c7e8f-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="c7e8f-287">13.75.152.195</span></span> | <span data-ttu-id="c7e8f-288">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-288">443</span></span> | <span data-ttu-id="c7e8f-289">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-290">Юго-Восточная часть Австралии</span><span class="sxs-lookup"><span data-stu-id="c7e8f-290">Australia Southeast</span></span> | <span data-ttu-id="c7e8f-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="c7e8f-291">13.77.2.56</span></span></br><span data-ttu-id="c7e8f-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="c7e8f-292">13.77.2.94</span></span> | <span data-ttu-id="c7e8f-293">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-293">443</span></span> | <span data-ttu-id="c7e8f-294">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-294">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-295">Бразилия</span><span class="sxs-lookup"><span data-stu-id="c7e8f-295">Brazil</span></span> | <span data-ttu-id="c7e8f-296">Южная часть Бразилии</span><span class="sxs-lookup"><span data-stu-id="c7e8f-296">Brazil South</span></span> | <span data-ttu-id="c7e8f-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="c7e8f-297">191.235.84.104</span></span></br><span data-ttu-id="c7e8f-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="c7e8f-298">191.235.87.113</span></span> | <span data-ttu-id="c7e8f-299">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-299">443</span></span> | <span data-ttu-id="c7e8f-300">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-300">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-301">Канада</span><span class="sxs-lookup"><span data-stu-id="c7e8f-301">Canada</span></span> | <span data-ttu-id="c7e8f-302">Восточная Канада</span><span class="sxs-lookup"><span data-stu-id="c7e8f-302">Canada East</span></span> | <span data-ttu-id="c7e8f-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="c7e8f-303">52.229.127.96</span></span></br><span data-ttu-id="c7e8f-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="c7e8f-304">52.229.123.172</span></span> | <span data-ttu-id="c7e8f-305">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-305">443</span></span> | <span data-ttu-id="c7e8f-306">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-307">Центральная Канада</span><span class="sxs-lookup"><span data-stu-id="c7e8f-307">Canada Central</span></span> | <span data-ttu-id="c7e8f-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="c7e8f-308">52.228.37.66</span></span></br><span data-ttu-id="c7e8f-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="c7e8f-309">52.228.45.222</span></span> | <span data-ttu-id="c7e8f-310">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-310">443</span></span> | <span data-ttu-id="c7e8f-311">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-311">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-312">Китай</span><span class="sxs-lookup"><span data-stu-id="c7e8f-312">China</span></span> | <span data-ttu-id="c7e8f-313">Север Китая</span><span class="sxs-lookup"><span data-stu-id="c7e8f-313">China North</span></span> | <span data-ttu-id="c7e8f-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="c7e8f-314">42.159.96.170</span></span></br><span data-ttu-id="c7e8f-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="c7e8f-315">139.217.2.219</span></span> | <span data-ttu-id="c7e8f-316">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-316">443</span></span> | <span data-ttu-id="c7e8f-317">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-318">Восток Китая</span><span class="sxs-lookup"><span data-stu-id="c7e8f-318">China East</span></span> | <span data-ttu-id="c7e8f-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="c7e8f-319">42.159.198.178</span></span></br><span data-ttu-id="c7e8f-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="c7e8f-320">42.159.234.157</span></span> | <span data-ttu-id="c7e8f-321">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-321">443</span></span> | <span data-ttu-id="c7e8f-322">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-322">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-323">Европа</span><span class="sxs-lookup"><span data-stu-id="c7e8f-323">Europe</span></span> | <span data-ttu-id="c7e8f-324">Северная Европа</span><span class="sxs-lookup"><span data-stu-id="c7e8f-324">North Europe</span></span> | <span data-ttu-id="c7e8f-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="c7e8f-325">52.164.210.96</span></span></br><span data-ttu-id="c7e8f-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="c7e8f-326">13.74.153.132</span></span> | <span data-ttu-id="c7e8f-327">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-327">443</span></span> | <span data-ttu-id="c7e8f-328">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-329">Западная Европа</span><span class="sxs-lookup"><span data-stu-id="c7e8f-329">West Europe</span></span>| <span data-ttu-id="c7e8f-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="c7e8f-330">52.166.243.90</span></span></br><span data-ttu-id="c7e8f-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="c7e8f-331">52.174.36.244</span></span> | <span data-ttu-id="c7e8f-332">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-332">443</span></span> | <span data-ttu-id="c7e8f-333">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-333">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-334">Германия</span><span class="sxs-lookup"><span data-stu-id="c7e8f-334">Germany</span></span> | <span data-ttu-id="c7e8f-335">Центральная Германия</span><span class="sxs-lookup"><span data-stu-id="c7e8f-335">Germany Central</span></span> | <span data-ttu-id="c7e8f-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="c7e8f-336">51.4.146.68</span></span></br><span data-ttu-id="c7e8f-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="c7e8f-337">51.4.146.80</span></span> | <span data-ttu-id="c7e8f-338">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-338">443</span></span> | <span data-ttu-id="c7e8f-339">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-340">Северо-восточная Германия</span><span class="sxs-lookup"><span data-stu-id="c7e8f-340">Germany Northeast</span></span> | <span data-ttu-id="c7e8f-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="c7e8f-341">51.5.150.132</span></span></br><span data-ttu-id="c7e8f-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="c7e8f-342">51.5.144.101</span></span> | <span data-ttu-id="c7e8f-343">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-343">443</span></span> | <span data-ttu-id="c7e8f-344">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-344">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-345">Индия</span><span class="sxs-lookup"><span data-stu-id="c7e8f-345">India</span></span> | <span data-ttu-id="c7e8f-346">Центральная Индия</span><span class="sxs-lookup"><span data-stu-id="c7e8f-346">Central India</span></span> | <span data-ttu-id="c7e8f-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="c7e8f-347">52.172.153.209</span></span></br><span data-ttu-id="c7e8f-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="c7e8f-348">52.172.152.49</span></span> | <span data-ttu-id="c7e8f-349">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-349">443</span></span> | <span data-ttu-id="c7e8f-350">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-350">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-351">Япония</span><span class="sxs-lookup"><span data-stu-id="c7e8f-351">Japan</span></span> | <span data-ttu-id="c7e8f-352">Восточная часть Японии</span><span class="sxs-lookup"><span data-stu-id="c7e8f-352">Japan East</span></span> | <span data-ttu-id="c7e8f-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="c7e8f-353">13.78.125.90</span></span></br><span data-ttu-id="c7e8f-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="c7e8f-354">13.78.89.60</span></span> | <span data-ttu-id="c7e8f-355">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-355">443</span></span> | <span data-ttu-id="c7e8f-356">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-357">Западная часть Японии</span><span class="sxs-lookup"><span data-stu-id="c7e8f-357">Japan West</span></span> | <span data-ttu-id="c7e8f-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="c7e8f-358">40.74.125.69</span></span></br><span data-ttu-id="c7e8f-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="c7e8f-359">138.91.29.150</span></span> | <span data-ttu-id="c7e8f-360">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-360">443</span></span> | <span data-ttu-id="c7e8f-361">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-361">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-362">Корея</span><span class="sxs-lookup"><span data-stu-id="c7e8f-362">Korea</span></span> | <span data-ttu-id="c7e8f-363">Центральная Корея</span><span class="sxs-lookup"><span data-stu-id="c7e8f-363">Korea Central</span></span> | <span data-ttu-id="c7e8f-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="c7e8f-364">52.231.39.142</span></span></br><span data-ttu-id="c7e8f-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="c7e8f-365">52.231.36.209</span></span> | <span data-ttu-id="c7e8f-366">433</span><span class="sxs-lookup"><span data-stu-id="c7e8f-366">433</span></span> | <span data-ttu-id="c7e8f-367">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-368">Южная Корея</span><span class="sxs-lookup"><span data-stu-id="c7e8f-368">Korea South</span></span> | <span data-ttu-id="c7e8f-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="c7e8f-369">52.231.203.16</span></span></br><span data-ttu-id="c7e8f-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="c7e8f-370">52.231.205.214</span></span> | <span data-ttu-id="c7e8f-371">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-371">443</span></span> | <span data-ttu-id="c7e8f-372">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-372">Inbound</span></span>
    | <span data-ttu-id="c7e8f-373">Великобритания</span><span class="sxs-lookup"><span data-stu-id="c7e8f-373">United Kingdom</span></span> | <span data-ttu-id="c7e8f-374">Западная часть Великобритании</span><span class="sxs-lookup"><span data-stu-id="c7e8f-374">UK West</span></span> | <span data-ttu-id="c7e8f-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="c7e8f-375">51.141.13.110</span></span></br><span data-ttu-id="c7e8f-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="c7e8f-376">51.141.7.20</span></span> | <span data-ttu-id="c7e8f-377">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-377">443</span></span> | <span data-ttu-id="c7e8f-378">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-379">Южная часть Великобритании</span><span class="sxs-lookup"><span data-stu-id="c7e8f-379">UK South</span></span> | <span data-ttu-id="c7e8f-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="c7e8f-380">51.140.47.39</span></span></br><span data-ttu-id="c7e8f-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="c7e8f-381">51.140.52.16</span></span> | <span data-ttu-id="c7e8f-382">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-382">443</span></span> | <span data-ttu-id="c7e8f-383">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-383">Inbound</span></span> |
    | <span data-ttu-id="c7e8f-384">США</span><span class="sxs-lookup"><span data-stu-id="c7e8f-384">United States</span></span> | <span data-ttu-id="c7e8f-385">Центральный регион США</span><span class="sxs-lookup"><span data-stu-id="c7e8f-385">Central US</span></span> | <span data-ttu-id="c7e8f-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="c7e8f-386">13.67.223.215</span></span></br><span data-ttu-id="c7e8f-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="c7e8f-387">40.86.83.253</span></span> | <span data-ttu-id="c7e8f-388">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-388">443</span></span> | <span data-ttu-id="c7e8f-389">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-390">Северо-центральный регион США</span><span class="sxs-lookup"><span data-stu-id="c7e8f-390">North Central US</span></span> | <span data-ttu-id="c7e8f-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="c7e8f-391">157.56.8.38</span></span></br><span data-ttu-id="c7e8f-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="c7e8f-392">157.55.213.99</span></span> | <span data-ttu-id="c7e8f-393">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-393">443</span></span> | <span data-ttu-id="c7e8f-394">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-395">Западно-центральная часть США</span><span class="sxs-lookup"><span data-stu-id="c7e8f-395">West Central US</span></span> | <span data-ttu-id="c7e8f-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="c7e8f-396">52.161.23.15</span></span></br><span data-ttu-id="c7e8f-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="c7e8f-397">52.161.10.167</span></span> | <span data-ttu-id="c7e8f-398">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-398">443</span></span> | <span data-ttu-id="c7e8f-399">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="c7e8f-400">Западный регион США 2</span><span class="sxs-lookup"><span data-stu-id="c7e8f-400">West US 2</span></span> | <span data-ttu-id="c7e8f-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="c7e8f-401">52.175.211.210</span></span></br><span data-ttu-id="c7e8f-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="c7e8f-402">52.175.222.222</span></span> | <span data-ttu-id="c7e8f-403">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-403">443</span></span> | <span data-ttu-id="c7e8f-404">Входящий трафик</span><span class="sxs-lookup"><span data-stu-id="c7e8f-404">Inbound</span></span> |

    <span data-ttu-id="c7e8f-405">На hello IP-адреса toouse для Azure для государственных, см. в разделе hello [аналитики Azure государственных + аналитика](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-405">For information on hello IP addresses toouse for Azure Government, see hello [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="c7e8f-406">Если в виртуальной сети используется пользовательский DNS-сервер, необходимо также разрешить доступ с адреса __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="c7e8f-407">Этот адрес рекурсивного сопоставителя Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="c7e8f-408">Дополнительные сведения см. в разделе hello [разрешение имен для виртуальных машин и роль экземпляров](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-408">For more information, see hello [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="c7e8f-409">Дополнительные сведения см. в разделе hello [управлению сетевым трафиком](#networktraffic) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-409">For more information, see hello [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="c7e8f-410"><a id="hdinsight-ports"></a> Требуемые порты</span><span class="sxs-lookup"><span data-stu-id="c7e8f-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="c7e8f-411">Если вы планируете использовать сеть **брандмауэра виртуальное устройство** toosecure hello виртуальной сети, необходимо разрешить исходящий трафик на hello, следующие порты:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-411">If you plan on using a network **virtual appliance firewall** toosecure hello virtual network, you must allow outbound traffic on hello following ports:</span></span>

* <span data-ttu-id="c7e8f-412">53</span><span class="sxs-lookup"><span data-stu-id="c7e8f-412">53</span></span>
* <span data-ttu-id="c7e8f-413">443</span><span class="sxs-lookup"><span data-stu-id="c7e8f-413">443</span></span>
* <span data-ttu-id="c7e8f-414">1433</span><span class="sxs-lookup"><span data-stu-id="c7e8f-414">1433</span></span>
* <span data-ttu-id="c7e8f-415">11000–11999;</span><span class="sxs-lookup"><span data-stu-id="c7e8f-415">11000-11999</span></span>
* <span data-ttu-id="c7e8f-416">14000–14999.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-416">14000-14999</span></span>

<span data-ttu-id="c7e8f-417">Список портов для определенных служб см. в разделе hello [порты, используемые службами Hadoop в HDInsight](hdinsight-hadoop-port-settings-for-services.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-417">For a list of ports for specific services, see hello [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="c7e8f-418">Дополнительные сведения о правила брандмауэра для виртуальных устройств см. в разделе hello [сценарий виртуальное устройство](../virtual-network/virtual-network-scenario-udr-gw-nva.md) документа.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-418">For more information on firewall rules for virtual appliances, see hello [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="c7e8f-419"><a id="hdinsight-nsg"></a>Пример: группы безопасности сети с HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7e8f-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="c7e8f-420">Hello в примерах этого раздела показано, как правила toocreate сетевой группы безопасности, позволяющие toocommunicate HDInsight с hello службы управления Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-420">hello examples in this section demonstrate how toocreate network security group rules that allow HDInsight toocommunicate with hello Azure management services.</span></span> <span data-ttu-id="c7e8f-421">При использовании примеров hello, настройте hello IP адресов toomatch hello из них для hello регион Azure, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-421">Before using hello examples, adjust hello IP addresses toomatch hello ones for hello Azure region you are using.</span></span> <span data-ttu-id="c7e8f-422">Эти сведения можно найти в hello [HDInsight с группами безопасности сети и определяемых пользователем маршрутов](#hdinsight-ip) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-422">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="c7e8f-423">Шаблон управления ресурсами Azure</span><span class="sxs-lookup"><span data-stu-id="c7e8f-423">Azure Resource Management template</span></span>

<span data-ttu-id="c7e8f-424">Hello следующий шаблон управления ресурсами создает виртуальной сети, которая ограничивает входящий трафик, но разрешает трафик с hello IP-адреса, необходимые для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-424">hello following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="c7e8f-425">Этот шаблон также создает кластер HDInsight в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-425">This template also creates an HDInsight cluster in hello virtual network.</span></span>

* [<span data-ttu-id="c7e8f-426">Развертывание защищенной виртуальной сети Azure и кластера HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="c7e8f-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="c7e8f-427">Изменение IP-адреса hello в этот примере toomatch hello регион Azure, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-427">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="c7e8f-428">Эти сведения можно найти в hello [HDInsight с группами безопасности сети и определяемых пользователем маршрутов](#hdinsight-ip) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-428">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="c7e8f-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7e8f-429">Azure PowerShell</span></span>

<span data-ttu-id="c7e8f-430">Используйте следующий сценарий PowerShell toocreate виртуальной сети, которая ограничивает входящего трафика и разрешает трафик с hello IP-адресов для Северной Европы hello hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-430">Use hello following PowerShell script toocreate a virtual network that restricts inbound traffic and allows traffic from hello IP addresses for hello North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7e8f-431">Изменение IP-адреса hello в этот примере toomatch hello регион Azure, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-431">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="c7e8f-432">Эти сведения можно найти в hello [HDInsight с группами безопасности сети и определяемых пользователем маршрутов](#hdinsight-ip) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-432">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="c7e8f-433">В этом примере показано, как tooallow tooadd правила входящего трафика на hello необходимых IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-433">This example demonstrates how tooadd rules tooallow inbound traffic on hello required IP addresses.</span></span> <span data-ttu-id="c7e8f-434">Не содержит toorestrict правило входящий доступ из других источников.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-434">It does not contain a rule toorestrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="c7e8f-435">Hello в следующем примере показано, как доступ к tooenable SSH из Интернета hello:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-435">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="c7e8f-436">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="c7e8f-436">Azure CLI</span></span>

<span data-ttu-id="c7e8f-437">Используйте следующие шаги toocreate виртуальной сети, которая ограничивает входящий трафик, но разрешает трафик с hello IP-адреса, необходимые для HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-437">Use hello following steps toocreate a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="c7e8f-438">Следующая команда toocreate новую группу безопасности сети с именем hello используйте `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-438">Use hello following command toocreate a new network security group named `hdisecure`.</span></span> <span data-ttu-id="c7e8f-439">Замените **RESOURCEGROUPNAME** с группой ресурсов hello, содержащий hello виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-439">Replace **RESOURCEGROUPNAME** with hello resource group that contains hello Azure Virtual Network.</span></span> <span data-ttu-id="c7e8f-440">Замените **РАСПОЛОЖЕНИЕ** с hello местоположение (регион) был создан этой группы hello в.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-440">Replace **LOCATION** with hello location (region) that hello group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="c7e8f-441">После создания группы hello вы получите информацию для новой группы hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-441">Once hello group has been created, you receive information on hello new group.</span></span>

2. <span data-ttu-id="c7e8f-442">Используйте следующие tooadd правила toohello новую группу безопасности сети, разрешить входящий трафик на порте 443 из службы работоспособности и управления Azure HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-442">Use hello following tooadd rules toohello new network security group that allow inbound communication on port 443 from hello Azure HDInsight health and management service.</span></span> <span data-ttu-id="c7e8f-443">Замените **RESOURCEGROUPNAME** с именем hello hello группы ресурсов, которая содержит hello виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-443">Replace **RESOURCEGROUPNAME** with hello name of hello resource group that contains hello Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c7e8f-444">Изменение IP-адреса hello в этот примере toomatch hello регион Azure, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-444">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="c7e8f-445">Эти сведения можно найти в hello [HDInsight с группами безопасности сети и определяемых пользователем маршрутов](#hdinsight-ip) раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-445">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="c7e8f-446">tooretrieve hello уникальный идентификатор для этой группы безопасности сети, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-446">tooretrieve hello unique identifier for this network security group, use hello following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="c7e8f-447">Эта команда возвращает аналогичные toohello значение, следующий текст:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-447">This command returns a value similar toohello following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="c7e8f-448">Используйте двойные кавычки вокруг идентификатор в команду hello, если не дал результатов ожидается hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-448">Use double-quotes around id in hello command if you don't get hello expected results.</span></span>

4. <span data-ttu-id="c7e8f-449">Используйте следующие команды tooapply hello безопасности группы tooa подсети hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-449">Use hello following command tooapply hello network security group tooa subnet.</span></span> <span data-ttu-id="c7e8f-450">Замените hello __GUID__ и __RESOURCEGROUPNAME__ значения с hello тех, которые возвращены из предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-450">Replace hello __GUID__ and __RESOURCEGROUPNAME__ values with hello ones returned from hello previous step.</span></span> <span data-ttu-id="c7e8f-451">Замените __VNETNAME__ и __SUBNETNAME__ с именем hello виртуальной сети и подсети, которые должны toocreate.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-451">Replace __VNETNAME__ and __SUBNETNAME__ with hello virtual network name and subnet name that you want toocreate.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="c7e8f-452">После выполнения этой команды можно установить HDInsight в hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-452">Once this command completes, you can install HDInsight into hello Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7e8f-453">Эти действия только открыть доступ toohello HDInsight работоспособности и управления службу hello облако Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-453">These steps only open access toohello HDInsight health and management service on hello Azure cloud.</span></span> <span data-ttu-id="c7e8f-454">Все другие доступа toohello кластер HDInsight из внешней hello виртуальной сети будет заблокирован.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-454">Any other access toohello HDInsight cluster from outside hello Virtual Network is blocked.</span></span> <span data-ttu-id="c7e8f-455">tooenable доступ из внешней hello виртуальной сети, необходимо добавить дополнительные правила группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-455">tooenable access from outside hello virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="c7e8f-456">Hello в следующем примере показано, как доступ к tooenable SSH из Интернета hello:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-456">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="c7e8f-457"><a id="example-dns"></a> Пример: конфигурация DNS</span><span class="sxs-lookup"><span data-stu-id="c7e8f-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="c7e8f-458">Разрешение DNS-имен между виртуальной сетью и подключенной локальной сетью</span><span class="sxs-lookup"><span data-stu-id="c7e8f-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="c7e8f-459">Этот пример делает hello следующие допущения:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-459">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="c7e8f-460">У вас есть виртуальная сеть Azure, подключенной tooan локальной сети с помощью шлюза VPN.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-460">You have an Azure Virtual Network that is connected tooan on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="c7e8f-461">Hello пользовательского DNS-сервера в виртуальной сети hello выполняется под hello операционной системы Unix или Linux.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-461">hello custom DNS server in hello virtual network is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="c7e8f-462">[Привязать](https://www.isc.org/downloads/bind/) устанавливается на hello пользовательского DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-462">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS server.</span></span>

<span data-ttu-id="c7e8f-463">На hello пользовательского DNS-сервера в виртуальной сети hello:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-463">On hello custom DNS server in hello virtual network:</span></span>

1. <span data-ttu-id="c7e8f-464">Используйте Azure PowerShell или Azure CLI toofind hello DNS-суффикс hello виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-464">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of hello virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="c7e8f-465">На hello пользовательского DNS-сервера для hello виртуальной сети, используйте hello после текста как содержимое hello hello `/etc/bind/named.conf.local` файла:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-465">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="c7e8f-466">Замените hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` значение с DNS-суффиксом hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-466">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="c7e8f-467">Эта конфигурация направляет все запросы DNS для DNS-суффикс hello hello виртуальной сети toohello Azure рекурсивного сопоставителя.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-467">This configuration routes all DNS requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver.</span></span>

2. <span data-ttu-id="c7e8f-468">На hello пользовательского DNS-сервера для hello виртуальной сети, используйте hello после текста как содержимое hello hello `/etc/bind/named.conf.options` файла:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-468">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="c7e8f-469">Замените hello `10.0.0.0/16` значение с hello диапазон IP-адресов виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-469">Replace hello `10.0.0.0/16` value with hello IP address range of your virtual network.</span></span> <span data-ttu-id="c7e8f-470">Эта запись разрешает запросы на разрешение имен в этом диапазоне.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="c7e8f-471">Добавить диапазон IP-адресов hello объекта hello в локальной сети toohello `acl goodclients { ... }` раздела.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-471">Add hello IP address range of hello on-premises network toohello `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="c7e8f-472">запись разрешает запросы разрешения имен из ресурсов в локальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-472">entry allows name resolution requests from resources in hello on-premises network.</span></span>
    
    * <span data-ttu-id="c7e8f-473">Замените значение hello `192.168.0.1` hello IP-адрес локального DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-473">Replace hello value `192.168.0.1` with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="c7e8f-474">Эта запись направляет все другие DNS запросы toohello локального DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-474">This entry routes all other DNS requests toohello on-premises DNS server.</span></span>

3. <span data-ttu-id="c7e8f-475">Конфигурация toouse hello, перезапустите привязки.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-475">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="c7e8f-476">Например, `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="c7e8f-477">Добавление условной пересылки toohello локальный DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-477">Add a conditional forwarder toohello on-premises DNS server.</span></span> <span data-ttu-id="c7e8f-478">Настройте запросы toosend hello условной пересылки DNS-суффикс hello из шага 1 toohello пользовательского DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-478">Configure hello conditional forwarder toosend requests for hello DNS suffix from step 1 toohello custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c7e8f-479">В документации hello программного обеспечения DNS конкретные сведения о том, как tooadd условной пересылки.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-479">Consult hello documentation for your DNS software for specifics on how tooadd a conditional forwarder.</span></span>

<span data-ttu-id="c7e8f-480">После выполнения этих действий, можно подключить tooresources в сети, либо используя полные доменные имена (FQDN).</span><span class="sxs-lookup"><span data-stu-id="c7e8f-480">After completing these steps, you can connect tooresources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="c7e8f-481">Теперь можно установить HDInsight в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-481">You can now install HDInsight into hello virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="c7e8f-482">Разрешение имен между двумя подключенными виртуальными сетями</span><span class="sxs-lookup"><span data-stu-id="c7e8f-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="c7e8f-483">Этот пример делает hello следующие допущения:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-483">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="c7e8f-484">Имеется две виртуальных сети Azure, подключенные друг к другу посредством VPN-шлюза или пиринга.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="c7e8f-485">Hello пользовательского DNS-сервера в обеих сетях выполняется под hello операционной системы Unix или Linux.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-485">hello custom DNS server in both networks is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="c7e8f-486">[Привязать](https://www.isc.org/downloads/bind/) устанавливается на hello пользовательские DNS-серверы.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-486">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS servers.</span></span>

1. <span data-ttu-id="c7e8f-487">Использование Azure PowerShell или Azure CLI toofind hello DNS-суффикс обе виртуальные сети:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-487">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="c7e8f-488">Используйте hello после текста как содержимое hello hello `/etc/bind/named.config.local` файл на hello пользовательского DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-488">Use hello following text as hello contents of hello `/etc/bind/named.config.local` file on hello custom DNS server.</span></span> <span data-ttu-id="c7e8f-489">Внести это изменение на hello пользовательского DNS-сервера в обе виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-489">Make this change on hello custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    <span data-ttu-id="c7e8f-490">Замените hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` значение с DNS-суффикс hello hello __других__ виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-490">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of hello __other__ virtual network.</span></span> <span data-ttu-id="c7e8f-491">Эта запись будет направлять запросы DNS-суффикс hello toohello удаленной сети hello пользовательские DNS-сервер в этой сети.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-491">This entry routes requests for hello DNS suffix of hello remote network toohello custom DNS in that network.</span></span>

3. <span data-ttu-id="c7e8f-492">На hello пользовательские DNS-серверы в обе виртуальные сети, с помощью hello после текста как содержимое hello hello `/etc/bind/named.conf.options` файла:</span><span class="sxs-lookup"><span data-stu-id="c7e8f-492">On hello custom DNS servers in both virtual networks, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="c7e8f-493">Замените hello `10.0.0.0/16` и `10.1.0.0/16` значения hello IP-адресов виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-493">Replace hello `10.0.0.0/16` and `10.1.0.0/16` values with hello IP address ranges of your virtual networks.</span></span> <span data-ttu-id="c7e8f-494">Эта запись позволяет ресурсы в каждой сети запросы toomake hello DNS-серверов.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-494">This entry allows resources in each network toomake requests of hello DNS servers.</span></span>

    <span data-ttu-id="c7e8f-495">Запросы, которые не предназначены для DNS-суффиксы hello hello виртуальных сетей (например, microsoft.com) обрабатывается hello Azure рекурсивного сопоставителя.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-495">Any requests that are not for hello DNS suffixes of hello virtual networks (for example, microsoft.com) is handled by hello Azure recursive resolver.</span></span>

4. <span data-ttu-id="c7e8f-496">Конфигурация toouse hello, перезапустите привязки.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-496">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="c7e8f-497">Например, `sudo service bind9 restart` на обоих DNS-серверах.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="c7e8f-498">После выполнения этих действий, можно подключить tooresources в hello виртуальной сети, используя полные доменные имена (FQDN).</span><span class="sxs-lookup"><span data-stu-id="c7e8f-498">After completing these steps, you can connect tooresources in hello virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="c7e8f-499">Теперь можно установить HDInsight в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8f-499">You can now install HDInsight into hello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7e8f-500">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c7e8f-500">Next steps</span></span>

* <span data-ttu-id="c7e8f-501">Пример конца в конец настройки HDInsight tooconnect tooan локальную сеть, в разделе [HDInsight подключения tooan локальной сети](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="c7e8f-501">For an end-to-end example of configuring HDInsight tooconnect tooan on-premises network, see [Connect HDInsight tooan on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="c7e8f-502">Дополнительные сведения о виртуальных сетях Azure см. в разделе hello [Обзор виртуальной сети Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7e8f-502">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="c7e8f-503">Дополнительные сведения о группах безопасности сети см. в статье [Фильтрация сетевого трафика с помощью групп безопасности сети](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="c7e8f-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="c7e8f-504">Дополнительные сведения о пользовательских маршрутах см. в статье [Определяемые пользователем маршруты и IP-пересылка](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7e8f-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>