---
title: "Ведение журнала tooflow aaaIntroduction для группы безопасности сети с Наблюдатель сети Azure | Документы Microsoft"
description: "На этой странице объясняется, как поток NSG toouse регистрирует функцию Наблюдатель сети Azure"
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
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a><span data-ttu-id="cbe9f-103">Ведение журнала tooflow введение для групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="cbe9f-103">Introduction tooflow logging for Network Security Groups</span></span>

<span data-ttu-id="cbe9f-104">Сетевая группа безопасности потока журналы являются возможностью Наблюдатель сети, который позволяет вам tooview сведения о входящего и исходящего IP-трафика через группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-104">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="cbe9f-105">Эти потока журналы записываются в формате json и Показать исходящих и входящих потоков на основе каждого правила hello потока hello сетевого Адаптера, применяется 5-фрагментному сведения о потоке hello (источник и назначение IP-адрес, порт источника или целевой Protocol) и если hello был разрешен трафик или запрещено.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

![Обзор журналов потоков][1]

<span data-ttu-id="cbe9f-107">Хотя поток входит в целевые группы безопасности сети, они не отображаются hello же, как hello другие журналы.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-107">While flow logs target Network Security Groups, they are not displayed hello same as hello other logs.</span></span> <span data-ttu-id="cbe9f-108">Поток журналы хранятся только в пределах учетной записи хранилища и следующий путь hello ведения журнала, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="cbe9f-108">Flow logs are stored only within a storage account and following hello logging path as shown in hello following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="cbe9f-109">Здравствуйте же политики хранения, как показано на другие журналы применить tooflow журналы.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-109">hello same retention policies as seen on other logs apply tooflow logs.</span></span> <span data-ttu-id="cbe9f-110">Журналы имеют политики хранения, может принимать значения от 1 дня too365 дней.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-110">Logs have a retention policy that can be set from 1 day too365 days.</span></span> <span data-ttu-id="cbe9f-111">Если политика хранения не задано, журналы hello сохраняются навсегда.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-111">If a retention policy is not set, hello logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="cbe9f-112">Файл журнала</span><span class="sxs-lookup"><span data-stu-id="cbe9f-112">Log file</span></span>

<span data-ttu-id="cbe9f-113">Журналы потоков имеют несколько свойств.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="cbe9f-114">Hello ниже приведен перечень hello свойства, которые возвращаются в hello NSG потока журнала.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-114">hello following list is a listing of hello properties that are returned within hello NSG flow log:</span></span>

* <span data-ttu-id="cbe9f-115">**время** — время, когда было зарегистрировано событие hello</span><span class="sxs-lookup"><span data-stu-id="cbe9f-115">**time** - Time when hello event was logged</span></span>
* <span data-ttu-id="cbe9f-116">**systemId** — идентификатор ресурса группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="cbe9f-117">**Категория** -категории hello hello события, это будет всегда быть NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="cbe9f-117">**category** - hello category of hello event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="cbe9f-118">**ResourceId** -hello hello NSG идентификатор ресурса</span><span class="sxs-lookup"><span data-stu-id="cbe9f-118">**resourceid** - hello resource Id of hello NSG</span></span>
* <span data-ttu-id="cbe9f-119">**operationName** — всегда имеет значение NetworkSecurityGroupFlowEvents.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="cbe9f-120">**свойства** -это коллекция свойств потока hello</span><span class="sxs-lookup"><span data-stu-id="cbe9f-120">**properties** - A collection of properties of hello flow</span></span>
    * <span data-ttu-id="cbe9f-121">**Версия** -номер версии схемы событий потока журнала hello</span><span class="sxs-lookup"><span data-stu-id="cbe9f-121">**Version** - Version number of hello Flow Log event schema</span></span>
    * <span data-ttu-id="cbe9f-122">**flows** — набор потоков.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="cbe9f-123">Это свойство имеет несколько записей для различных ролей.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="cbe9f-124">**правило** -правило, для которых hello перечислены потоки</span><span class="sxs-lookup"><span data-stu-id="cbe9f-124">**rule** - Rule for which hello flows are listed</span></span>
            * <span data-ttu-id="cbe9f-125">**flows** — набор потоков.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="cbe9f-126">**Mac** -hello MAC-адрес hello сетевой Адаптер для виртуальной Машины, где были собраны потока hello hello</span><span class="sxs-lookup"><span data-stu-id="cbe9f-126">**mac** - hello MAC address of hello NIC for hello VM where hello flow was collected</span></span>
                * <span data-ttu-id="cbe9f-127">**flowTuples** -строка, содержащая несколько свойств для hello кортежа поток в формате с разделителями запятыми</span><span class="sxs-lookup"><span data-stu-id="cbe9f-127">**flowTuples** - A string that contains multiple properties for hello flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="cbe9f-128">**Штамп времени** -это значение равно hello отметку времени возникновения hello поток в формате ЭПОХИ UNIX</span><span class="sxs-lookup"><span data-stu-id="cbe9f-128">**Time Stamp** - This value is hello time stamp of when hello flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="cbe9f-129">**Исходный IP-адрес** - hello исходный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="cbe9f-129">**Source IP** - hello source IP</span></span>
                    * <span data-ttu-id="cbe9f-130">**Конечный IP** -hello конечный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="cbe9f-130">**Destination IP** - hello destination IP</span></span>
                    * <span data-ttu-id="cbe9f-131">**Исходный порт** - hello порт источника</span><span class="sxs-lookup"><span data-stu-id="cbe9f-131">**Source Port** - hello source port</span></span>
                    * <span data-ttu-id="cbe9f-132">**Порт назначения** -hello порт назначения</span><span class="sxs-lookup"><span data-stu-id="cbe9f-132">**Destination Port** - hello destination Port</span></span>
                    * <span data-ttu-id="cbe9f-133">**Протокол** -hello протокола hello потока.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-133">**Protocol** - hello protocol of hello flow.</span></span> <span data-ttu-id="cbe9f-134">Допустимые значения: **T** для протокола TCP и **U** для протокола UDP.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="cbe9f-135">**Поток трафика** -hello направление потока трафика hello.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-135">**Traffic Flow** - hello direction of hello traffic flow.</span></span> <span data-ttu-id="cbe9f-136">Допустимые значения: **I** для входящего трафика и **O** для исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="cbe9f-137">**Traffic** — указывает, разрешен или запрещен трафик.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="cbe9f-138">Допустимые значения: **A**, если трафик разрешен, и **D**, если запрещен.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="cbe9f-139">Hello ниже приведен пример журнала потока.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-139">hello following is an example of a Flow log.</span></span> <span data-ttu-id="cbe9f-140">Как видно, что имеется несколько записей, следующие за hello список свойств, описанных в предшествующих раздел hello.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-140">As you can see there are multiple records that follow hello property list described in hello preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="cbe9f-141">Значения в свойстве flowTuples hello: список с разделителями запятыми.</span><span class="sxs-lookup"><span data-stu-id="cbe9f-141">Values in hello flowTuples property are a comma-separated list.</span></span>
 
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

## <a name="next-steps"></a><span data-ttu-id="cbe9f-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cbe9f-142">Next steps</span></span>

<span data-ttu-id="cbe9f-143">Узнайте, каким образом ведет журнал tooenable потока, посетив [потока Включение ведения журнала](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cbe9f-143">Learn how tooenable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="cbe9f-144">Дополнительные сведения о ведении журнала NSG см. в разделе [Аналитика журналов для групп безопасности сети](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="cbe9f-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="cbe9f-145">Сведения о том, как узнать, разрешен или запрещен трафик на виртуальной машине, см. в разделе [Проверка состояния входящего и исходящего трафика виртуальной машины (разрешен или запрещен) путем проверки IP-потока (компонент Наблюдателя за сетями Azure)](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cbe9f-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

