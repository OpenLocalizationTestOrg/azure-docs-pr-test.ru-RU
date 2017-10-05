---
title: "Настройка режима распределения балансировщика нагрузки | Документация Майкрософт"
description: "Как настроить режим распределения подсистемы балансировки нагрузки Azure для поддержки соответствия исходному IP-адресу"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 4cb000c8ee1bb2e267dc0813dab23a77a46080ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-distribution-mode-for-load-balancer"></a><span data-ttu-id="7d0ae-103">Настройка режима распределения для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="7d0ae-103">Configure the distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="7d0ae-104">Режим распространения на основе хэша</span><span class="sxs-lookup"><span data-stu-id="7d0ae-104">Hash-based distribution mode</span></span>

<span data-ttu-id="7d0ae-105">В основе алгоритма распределения по умолчанию лежит использование хэша пяти кортежей (исходный IP-адрес, порт источника, IP-адрес назначения, порт назначения, тип протокола) для сопоставления трафика с доступными серверами.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-105">The default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span></span> <span data-ttu-id="7d0ae-106">Он позволяет закреплять IP-адреса только в рамках сеанса транспорта.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="7d0ae-107">Пакеты в рамках одного сеанса будут направляться на один экземпляр IP-адреса центра обработки данных в конечной точке с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-107">Packets in the same session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span></span> <span data-ttu-id="7d0ae-108">Когда клиент начинает новый сеанс с того же исходного IP-адреса, порт источника изменяется и перенаправляет трафик к другой конечной точке IP-адреса центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-108">When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span></span>

![подсистема балансировки нагрузки на основе хэша](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="7d0ae-110">Рис. 1. Пятикортежное распределение</span><span class="sxs-lookup"><span data-stu-id="7d0ae-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="7d0ae-111">Режим сходства исходного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="7d0ae-111">Source IP affinity mode</span></span>

<span data-ttu-id="7d0ae-112">Доступен новый режим распределения — соответствие исходному IP-адресу (также известный как соответствие сеансу или соответствие клиентскому IP-адресу).</span><span class="sxs-lookup"><span data-stu-id="7d0ae-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="7d0ae-113">С помощью этого режима Azure Load Balancer можно настроить для использования двух кортежей (исходный IP-адрес, IP-адрес назначения) или трех кортежей (исходный IP-адрес, IP-адрес назначения, протокол), чтобы сопоставлять трафик с доступными серверами.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-113">Azure Load Balancer can be configured to use a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) to map traffic to the available servers.</span></span> <span data-ttu-id="7d0ae-114">При использовании соответствия исходному IP-адресу подключения, инициированные с одного клиентского компьютера, направляются к одной конечной точке DIP.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-114">By using Source IP affinity, connections initiated from the same client computer goes to the same DIP endpoint.</span></span>

<span data-ttu-id="7d0ae-115">Конфигурация двухкортежного распределения представлена на следующей схеме.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-115">The following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="7d0ae-116">Обратите внимание, как два кортежа передаются через подсистему балансировки нагрузки на виртуальную машину 1 (VM1), а затем архивируются на виртуальных машинах VM2 и VM3.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-116">Notice how the 2-tuple runs through the load balancer to virtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![Сходство сеансов](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="7d0ae-118">Рис. 2. Двухкортежное распределение</span><span class="sxs-lookup"><span data-stu-id="7d0ae-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="7d0ae-119">Режим соответствия исходному IP-адресу позволяет устранить несовместимость подсистемы Azure Load Balancer и шлюза удаленных рабочих столов.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-119">Source IP affinity solves an incompatibility between the Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="7d0ae-120">Теперь можно создать ферму шлюза удаленных рабочих столов в одной облачной службе.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="7d0ae-121">Другой сценарий использования — передача мультимедиа, при которой передача данных осуществляется по протоколу UDP, а управление — по протоколу TCP.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-121">Another use case scenario is media upload where the data upload happens through UDP but the control plane is achieved through TCP:</span></span>

* <span data-ttu-id="7d0ae-122">Сначала клиент инициирует сеанс TCP для общедоступного IP-адреса с балансировкой нагрузки. Этот запрос отправляется по конкретному DIP, а сам канал остается активным, чтобы контролировать состояние подключения.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-122">A client first initiates a TCP session to the load balanced public address, gets directed to a specific DIP, this channel is left active to monitor the connection health</span></span>
* <span data-ttu-id="7d0ae-123">С того же клиентского компьютера для той же общедоступной конечной точки с балансировкой нагрузки инициируется новый сеанс UDP. Ожидается, что это подключение будет направлено на ту же конечную точку DIP, что и предыдущее TCP-подключение. Таким образом можно передавать мультимедиа с более высокой пропускной способностью, поддерживая при этом канал управления по TCP.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-123">A new UDP session from the same client computer is initiated to the same load balanced public endpoint, the expectation here is that this connection is also directed to the same DIP endpoint as the previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="7d0ae-124">При изменении набора балансировки нагрузки (при добавлении или удалении виртуальной машины) распределение запросов клиента вычисляется заново.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-124">When a load-balanced set changes (removing or adding a virtual machine), the distribution of client requests is recomputed.</span></span> <span data-ttu-id="7d0ae-125">Нельзя полагаться на то, что новые подключения от существующих клиентов будут направлены на один сервер.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-125">You cannot depend on new connections from existing clients ending up at the same server.</span></span> <span data-ttu-id="7d0ae-126">Кроме того, использование режима распределения соответствия исходному IP-адресу может привести к неравномерному распределению трафика.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="7d0ae-127">Клиенты, работающие на прокси-серверах, могут рассматриваться как одно уникальное клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="7d0ae-128">Настройка параметров соответствия исходному IP-адресу для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="7d0ae-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="7d0ae-129">Для виртуальных машин можно использовать PowerShell, чтобы изменить параметры времени ожидания:</span><span class="sxs-lookup"><span data-stu-id="7d0ae-129">For virtual machines, you can use PowerShell to change timeout settings:</span></span>

<span data-ttu-id="7d0ae-130">Добавление конечной точки Azure в виртуальную машину и установка режима распределения балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="7d0ae-130">Add an Azure endpoint to a Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="7d0ae-131">Параметру LoadBalancerDistribution можно присвоить следующие значения: sourceIP для балансировки нагрузки по двум кортежам (исходный IP-адрес, IP-адрес назначения); sourceIPProtocol для балансировки нагрузки по трем кортежам (исходный IP-адрес, IP-адрес назначения, протокол); none для поведения по умолчанию (балансировка нагрузки по пяти кортежам).</span><span class="sxs-lookup"><span data-stu-id="7d0ae-131">LoadBalancerDistribution can be set to sourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want the default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="7d0ae-132">Используйте следующий сценарий, чтобы получить конфигурацию режима распределения подсистемы балансировки нагрузки для конечной точки.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-132">Use the following to retrieve an endpoint load balancer distribution mode configuration:</span></span>

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15
    LoadBalancerDistribution : sourceIP

<span data-ttu-id="7d0ae-133">Если элемент LoadBalancerDistribution отсутствует, подсистема балансировки нагрузки Azure использует алгоритм балансировки нагрузки по умолчанию (балансировка нагрузки по 5 кортежам).</span><span class="sxs-lookup"><span data-stu-id="7d0ae-133">If the LoadBalancerDistribution element is not present then the Azure Load balancer uses the default 5-tuple algorithm.</span></span>

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="7d0ae-134">Установка режима распределения для набора балансировки нагрузки для конечных точек</span><span class="sxs-lookup"><span data-stu-id="7d0ae-134">Set the Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="7d0ae-135">Если набор балансировки нагрузки для конечных точек содержит конечные точки, для него следует установить режим распределения:</span><span class="sxs-lookup"><span data-stu-id="7d0ae-135">If endpoints are part of a load balanced endpoint set, the distribution mode must be set on the load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a><span data-ttu-id="7d0ae-136">Настройка облачной службы для изменения режима распределения</span><span class="sxs-lookup"><span data-stu-id="7d0ae-136">Cloud Service configuration to change distribution mode</span></span>

<span data-ttu-id="7d0ae-137">Вы можете обновить облачную службу с помощью пакета Azure SDK для .NET 2.5 (выпуск ожидается в ноябре).</span><span class="sxs-lookup"><span data-stu-id="7d0ae-137">You can leverage the Azure SDK for .NET 2.5 (to be released in November) to update your Cloud Service.</span></span> <span data-ttu-id="7d0ae-138">Конечные точки для облачных служб можно настроить в CSDEF-файле.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-138">Endpoint settings for Cloud Services are made in the .csdef.</span></span> <span data-ttu-id="7d0ae-139">Чтобы обновить режим распределения балансировщика нагрузки для развертывания облачных служб, нужно обновить развертывание.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-139">In order to update the load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="7d0ae-140">Ниже приведен пример изменений в CSDEF-файле для настройки конечных точек:</span><span class="sxs-lookup"><span data-stu-id="7d0ae-140">Here is an example of .csdef changes for endpoint settings:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
<InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
    <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
</InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="api-example"></a><span data-ttu-id="7d0ae-141">Пример API</span><span class="sxs-lookup"><span data-stu-id="7d0ae-141">API example</span></span>

<span data-ttu-id="7d0ae-142">Можно настроить распределение балансировщика нагрузки с помощью API управления службами.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-142">You can configure the load balancer distribution using the service management API.</span></span> <span data-ttu-id="7d0ae-143">Обязательно добавьте заголовок `x-ms-version`, для которого задана версия `2014-09-01` или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="7d0ae-143">Make sure to add the `x-ms-version` header is set to version `2014-09-01` or higher.</span></span>

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="7d0ae-144">Обновление конфигурации указанного набора балансировки нагрузки в развертывании</span><span class="sxs-lookup"><span data-stu-id="7d0ae-144">Update the configuration of the specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="7d0ae-145">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="7d0ae-145">Request example</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

<span data-ttu-id="7d0ae-146">Параметр LoadBalancerDistribution может иметь следующие значения: sourceIP для соответствия по двум кортежам; sourceIPProtocol для соответствия по трем кортежам; none (для отсутствия соответствия,</span><span class="sxs-lookup"><span data-stu-id="7d0ae-146">The value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="7d0ae-147">т. е. балансировки по пяти кортежам).</span><span class="sxs-lookup"><span data-stu-id="7d0ae-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="7d0ae-148">Ответ</span><span class="sxs-lookup"><span data-stu-id="7d0ae-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="7d0ae-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7d0ae-149">Next Steps</span></span>

[<span data-ttu-id="7d0ae-150">Обзор внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="7d0ae-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="7d0ae-151">Приступая к настройке подсистемы балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="7d0ae-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="7d0ae-152">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="7d0ae-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
