---
title: "Общие сведения о ведении журналов потоков для групп безопасности сети с помощью Наблюдателя за сетями | Документация Майкрософт"
description: "На этой странице объясняется, как использовать возможности журналов потоков NSG, доступные в Наблюдателе за сетями Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b7a9162d6c6219b6b1c51a49cd34b9616e9d3e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-flow-logging-for-network-security-groups"></a><span data-ttu-id="7c0ea-103">Общие сведения о ведении журнала потоков для групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="7c0ea-103">Introduction to flow logging for Network Security Groups</span></span>

<span data-ttu-id="7c0ea-104">Журналы потоков для групп безопасности сети — это компонент Наблюдателя за сетями, который позволяет просматривать сведения о входящем и исходящем IP-трафике через группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-104">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="7c0ea-105">Эти журналы потоков записываются в формате JSON. В них отображаются входящие и исходящие потоки по каждому правилу, сетевая карта, с которой связан поток, сведения о 5 кортежах потока (исходный и конечный IP-адреса, исходный и конечный порты, протокол), а также сведения о состоянии трафика (разрешен или запрещен).</span><span class="sxs-lookup"><span data-stu-id="7c0ea-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

![Обзор журналов потоков][1]

<span data-ttu-id="7c0ea-107">Хотя журналы потоков нацелены на группы безопасности сети, они не отображаются так же, как другие журналы.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-107">While flow logs target Network Security Groups, they are not displayed the same as the other logs.</span></span> <span data-ttu-id="7c0ea-108">Журналы потоков хранятся только в пределах учетной записи хранения и используют путь для ведения журнала, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-108">Flow logs are stored only within a storage account and following the logging path as shown in the following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="7c0ea-109">К журналам потоков применяются те же политики хранения, что и к другим журналам.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-109">The same retention policies as seen on other logs apply to flow logs.</span></span> <span data-ttu-id="7c0ea-110">Для журналов действует политика хранения, в которой можно задать период от 1 до 365 дней.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-110">Logs have a retention policy that can be set from 1 day to 365 days.</span></span> <span data-ttu-id="7c0ea-111">Если политика хранения не задана, то журналы сохраняются неограниченно долго.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-111">If a retention policy is not set, the logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="7c0ea-112">Файл журнала</span><span class="sxs-lookup"><span data-stu-id="7c0ea-112">Log file</span></span>

<span data-ttu-id="7c0ea-113">Журналы потоков имеют несколько свойств.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="7c0ea-114">Ниже приведен список свойств, которые возвращаются в журнале потоков NSG.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-114">The following list is a listing of the properties that are returned within the NSG flow log:</span></span>

* <span data-ttu-id="7c0ea-115">**time** — время занесения события в журнал.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-115">**time** - Time when the event was logged</span></span>
* <span data-ttu-id="7c0ea-116">**systemId** — идентификатор ресурса группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="7c0ea-117">**category** — категории события. Всегда будет иметь значение NetworkSecurityGroupFlowEvent.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-117">**category** - The category of the event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="7c0ea-118">**resourceid** — идентификатор ресурса NSG.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-118">**resourceid** - The resource Id of the NSG</span></span>
* <span data-ttu-id="7c0ea-119">**operationName** — всегда имеет значение NetworkSecurityGroupFlowEvents.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="7c0ea-120">**properties** — набор свойств потока.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-120">**properties** - A collection of properties of the flow</span></span>
    * <span data-ttu-id="7c0ea-121">**Version** — номер версии схемы событий журнала потоков.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-121">**Version** - Version number of the Flow Log event schema</span></span>
    * <span data-ttu-id="7c0ea-122">**flows** — набор потоков.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="7c0ea-123">Это свойство имеет несколько записей для различных ролей.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="7c0ea-124">**rule** — правило, для которого отображены потоки.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-124">**rule** - Rule for which the flows are listed</span></span>
            * <span data-ttu-id="7c0ea-125">**flows** — набор потоков.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="7c0ea-126">**mac** — MAC-адрес сетевой карты виртуальной машины, в которой был получен поток.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span></span>
                * <span data-ttu-id="7c0ea-127">**flowTuples** — строка с разделителями-запятыми, содержащая несколько свойств кортежа потока.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="7c0ea-128">**Time Stamp** — это значение представляет собой метку времени возникновения потока в формате UNIX EPOCH.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="7c0ea-129">**Source IP** — исходный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-129">**Source IP** - The source IP</span></span>
                    * <span data-ttu-id="7c0ea-130">**Destination IP** — конечный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-130">**Destination IP** - The destination IP</span></span>
                    * <span data-ttu-id="7c0ea-131">**Source Port** — исходный порт.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-131">**Source Port** - The source port</span></span>
                    * <span data-ttu-id="7c0ea-132">**Destination Port** — конечный порт.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-132">**Destination Port** - The destination Port</span></span>
                    * <span data-ttu-id="7c0ea-133">**Protocol** — протокол потока.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-133">**Protocol** - The protocol of the flow.</span></span> <span data-ttu-id="7c0ea-134">Допустимые значения: **T** для протокола TCP и **U** для протокола UDP.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="7c0ea-135">**Traffic Flow** — направление потока трафика.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-135">**Traffic Flow** - The direction of the traffic flow.</span></span> <span data-ttu-id="7c0ea-136">Допустимые значения: **I** для входящего трафика и **O** для исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="7c0ea-137">**Traffic** — указывает, разрешен или запрещен трафик.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="7c0ea-138">Допустимые значения: **A**, если трафик разрешен, и **D**, если запрещен.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="7c0ea-139">Ниже приведен пример журнала потоков.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-139">The following is an example of a Flow log.</span></span> <span data-ttu-id="7c0ea-140">Как вы видите, он содержит несколько записей, соответствующих списку свойств, описанных в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-140">As you can see there are multiple records that follow the property list described in the preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="7c0ea-141">Значения в свойстве flowTuples имеют вид списка с разделителями-запятыми.</span><span class="sxs-lookup"><span data-stu-id="7c0ea-141">Values in the flowTuples property are a comma-separated list.</span></span>
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a><span data-ttu-id="7c0ea-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c0ea-142">Next steps</span></span>

<span data-ttu-id="7c0ea-143">Узнайте, как включить журналы потоков, ознакомившись с разделом [Включение журналов потоков](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7c0ea-143">Learn how to enable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="7c0ea-144">Дополнительные сведения о ведении журнала NSG см. в разделе [Аналитика журналов для групп безопасности сети](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="7c0ea-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="7c0ea-145">Сведения о том, как узнать, разрешен или запрещен трафик на виртуальной машине, см. в разделе [Проверка состояния входящего и исходящего трафика виртуальной машины (разрешен или запрещен) путем проверки IP-потока (компонент Наблюдателя за сетями Azure)](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7c0ea-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

