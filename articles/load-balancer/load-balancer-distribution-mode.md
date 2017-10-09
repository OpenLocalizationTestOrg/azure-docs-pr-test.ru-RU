---
title: "режим распространения подсистемы балансировки нагрузки aaaConfigure | Документы Microsoft"
description: "Как tooconfigure Azure загрузить принадлежность IP источника toosupport режим балансировки распространения"
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
ms.openlocfilehash: e745240b733ffc07928d8ed0ae097785ad4f412e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-distribution-mode-for-load-balancer"></a><span data-ttu-id="6ded0-103">Настройка режима hello распространения для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="6ded0-103">Configure hello distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="6ded0-104">Режим распространения на основе хэша</span><span class="sxs-lookup"><span data-stu-id="6ded0-104">Hash-based distribution mode</span></span>

<span data-ttu-id="6ded0-105">алгоритм распределения Hello по умолчанию — 5-фрагментному (исходный IP-адрес, порт источника тип протокола конечный IP-адрес, порт назначения) хэш-серверы tooavailable toomap трафика.</span><span class="sxs-lookup"><span data-stu-id="6ded0-105">hello default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash toomap traffic tooavailable servers.</span></span> <span data-ttu-id="6ded0-106">Он позволяет закреплять IP-адреса только в рамках сеанса транспорта.</span><span class="sxs-lookup"><span data-stu-id="6ded0-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="6ded0-107">Пакетов в hello того же сеанса, будут направляться toohello экземпляра центра обработки данных IP-адрес (DIP) за конечной точкой с балансировкой нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="6ded0-107">Packets in hello same session will be directed toohello same datacenter IP (DIP) instance behind hello load balanced endpoint.</span></span> <span data-ttu-id="6ded0-108">При запуске клиента hello новый сеанс из Здравствуйте же исходный IP-адрес, порт источника hello изменяется в результате чего hello трафика toogo tooa другой DIP-адрес конечной точки.</span><span class="sxs-lookup"><span data-stu-id="6ded0-108">When hello client starts a new session from hello same source IP, hello source port changes and causes hello traffic toogo tooa different DIP endpoint.</span></span>

![подсистема балансировки нагрузки на основе хэша](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="6ded0-110">Рис. 1. Пятикортежное распределение</span><span class="sxs-lookup"><span data-stu-id="6ded0-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="6ded0-111">Режим сходства исходного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="6ded0-111">Source IP affinity mode</span></span>

<span data-ttu-id="6ded0-112">Доступен новый режим распределения — соответствие исходному IP-адресу (также известный как соответствие сеансу или соответствие клиентскому IP-адресу).</span><span class="sxs-lookup"><span data-stu-id="6ded0-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="6ded0-113">Подсистема балансировки нагрузки Azure может быть настроенный toouse кортеж из двух (исходный IP-адрес, конечный IP-адрес) или toomap (исходный IP-адрес, конечный IP-адрес, протокол) кортежа трафика toohello доступных серверов.</span><span class="sxs-lookup"><span data-stu-id="6ded0-113">Azure Load Balancer can be configured toouse a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) toomap traffic toohello available servers.</span></span> <span data-ttu-id="6ded0-114">С помощью сходства исходный IP-адрес, подключений инициированный hello же клиентский компьютер проходит toohello DIP-адрес конечной точки.</span><span class="sxs-lookup"><span data-stu-id="6ded0-114">By using Source IP affinity, connections initiated from hello same client computer goes toohello same DIP endpoint.</span></span>

<span data-ttu-id="6ded0-115">Следующая схема Hello показана конфигурация двух кортежей.</span><span class="sxs-lookup"><span data-stu-id="6ded0-115">hello following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="6ded0-116">Обратите внимание на то, как кортеж hello завершит hello нагрузки балансировки toovirtual машины 1 (VM1) которого затем резервной копии, созданной VM2 и VM3.</span><span class="sxs-lookup"><span data-stu-id="6ded0-116">Notice how hello 2-tuple runs through hello load balancer toovirtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![Сходство сеансов](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="6ded0-118">Рис. 2. Двухкортежное распределение</span><span class="sxs-lookup"><span data-stu-id="6ded0-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="6ded0-119">Сопоставление источника IP решает несовместимости hello подсистемы балансировки нагрузки Azure и шлюза удаленных рабочих столов (RD).</span><span class="sxs-lookup"><span data-stu-id="6ded0-119">Source IP affinity solves an incompatibility between hello Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="6ded0-120">Теперь можно создать ферму шлюза удаленных рабочих столов в одной облачной службе.</span><span class="sxs-lookup"><span data-stu-id="6ded0-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="6ded0-121">Другой вариант сценария использования — передача мультимедиа, где hello передача данных происходит через UDP, но hello плоскости управления достигается с помощью TCP:</span><span class="sxs-lookup"><span data-stu-id="6ded0-121">Another use case scenario is media upload where hello data upload happens through UDP but hello control plane is achieved through TCP:</span></span>

* <span data-ttu-id="6ded0-122">Клиент инициирует сеанс TCP с балансировкой нагрузки toohello общедоступный адрес, сначала возвращает расширенный tooa конкретных DIP, этот канал является работоспособность подключения левой active toomonitor hello</span><span class="sxs-lookup"><span data-stu-id="6ded0-122">A client first initiates a TCP session toohello load balanced public address, gets directed tooa specific DIP, this channel is left active toomonitor hello connection health</span></span>
* <span data-ttu-id="6ded0-123">Новый сеанс UDP из hello же клиент запустил toohello общедоступную конечную точку с балансировкой нагрузки на одном, hello здесь ожидается этого подключения также является направленным toohello DIP-адрес конечной точки предыдущего TCP-соединение hello, чтобы передать носитель может быть выполнен на высокую пропускную способность, сохраняя канал управления через TCP.</span><span class="sxs-lookup"><span data-stu-id="6ded0-123">A new UDP session from hello same client computer is initiated toohello same load balanced public endpoint, hello expectation here is that this connection is also directed toohello same DIP endpoint as hello previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="6ded0-124">При изменении набора с балансировкой нагрузки (или удалении виртуальной машины) будет пересчитано hello распределения запросов клиентов.</span><span class="sxs-lookup"><span data-stu-id="6ded0-124">When a load-balanced set changes (removing or adding a virtual machine), hello distribution of client requests is recomputed.</span></span> <span data-ttu-id="6ded0-125">Не следует рассчитывать новые соединения из существующих клиентов, попадающих в hello же сервера.</span><span class="sxs-lookup"><span data-stu-id="6ded0-125">You cannot depend on new connections from existing clients ending up at hello same server.</span></span> <span data-ttu-id="6ded0-126">Кроме того, использование режима распределения соответствия исходному IP-адресу может привести к неравномерному распределению трафика.</span><span class="sxs-lookup"><span data-stu-id="6ded0-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="6ded0-127">Клиенты, работающие на прокси-серверах, могут рассматриваться как одно уникальное клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="6ded0-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="6ded0-128">Настройка параметров соответствия исходному IP-адресу для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="6ded0-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="6ded0-129">Для виртуальных машин можно использовать параметры времени ожидания toochange PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6ded0-129">For virtual machines, you can use PowerShell toochange timeout settings:</span></span>

<span data-ttu-id="6ded0-130">Добавление конечной точки Azure tooa виртуальную машину и установите режим распространения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="6ded0-130">Add an Azure endpoint tooa Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="6ded0-131">LoadBalancerDistribution можно задать toosourceIP для двух кортежей (исходный IP-адрес, конечный IP-адрес), балансировка нагрузки sourceIPProtocol для балансировки нагрузки (исходный IP-адрес, конечный IP-адрес, протокол) кортежа или none, если необходимо поведение по умолчанию hello 5-фрагментному балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="6ded0-131">LoadBalancerDistribution can be set toosourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want hello default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="6ded0-132">Используйте следующие tooretrieve конфигурации конечной точки распространения подсистемы балансировки нагрузки режим hello.</span><span class="sxs-lookup"><span data-stu-id="6ded0-132">Use hello following tooretrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="6ded0-133">Если отсутствует элемент LoadBalancerDistribution hello hello балансировки нагрузки Azure использует алгоритм 5-фрагментному по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="6ded0-133">If hello LoadBalancerDistribution element is not present then hello Azure Load balancer uses hello default 5-tuple algorithm.</span></span>

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="6ded0-134">Установить режим распространения hello для набора конечных точек с балансировкой нагрузки</span><span class="sxs-lookup"><span data-stu-id="6ded0-134">Set hello Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="6ded0-135">Если конечные точки являются частью набора конечных точек с балансировкой нагрузки, режим распространения hello необходимо установить на набор конечных точек с балансировкой нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="6ded0-135">If endpoints are part of a load balanced endpoint set, hello distribution mode must be set on hello load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a><span data-ttu-id="6ded0-136">Облачные службы конфигурации toochange распространения режим</span><span class="sxs-lookup"><span data-stu-id="6ded0-136">Cloud Service configuration toochange distribution mode</span></span>

<span data-ttu-id="6ded0-137">Вы можете использовать hello Azure SDK для .NET 2.5 (toobe выпущенных в ноябре) tooupdate облачной службы.</span><span class="sxs-lookup"><span data-stu-id="6ded0-137">You can leverage hello Azure SDK for .NET 2.5 (toobe released in November) tooupdate your Cloud Service.</span></span> <span data-ttu-id="6ded0-138">Параметры конечной точки для облачных служб, выполняемых в hello .csdef.</span><span class="sxs-lookup"><span data-stu-id="6ded0-138">Endpoint settings for Cloud Services are made in hello .csdef.</span></span> <span data-ttu-id="6ded0-139">В порядке tooupdate hello балансировки режим распределения нагрузки развертывания облачных служб требуется обновление развертывания.</span><span class="sxs-lookup"><span data-stu-id="6ded0-139">In order tooupdate hello load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="6ded0-140">Ниже приведен пример изменений в CSDEF-файле для настройки конечных точек:</span><span class="sxs-lookup"><span data-stu-id="6ded0-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="6ded0-141">Пример API</span><span class="sxs-lookup"><span data-stu-id="6ded0-141">API example</span></span>

<span data-ttu-id="6ded0-142">Вы можете настроить распространение подсистемы балансировки нагрузки hello, с помощью API управления службами hello.</span><span class="sxs-lookup"><span data-stu-id="6ded0-142">You can configure hello load balancer distribution using hello service management API.</span></span> <span data-ttu-id="6ded0-143">Убедитесь, что hello tooadd `x-ms-version` задан заголовок tooversion `2014-09-01` или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6ded0-143">Make sure tooadd hello `x-ms-version` header is set tooversion `2014-09-01` or higher.</span></span>

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="6ded0-144">Обновление конфигурации hello hello указан набор балансировки нагрузки в развертывании</span><span class="sxs-lookup"><span data-stu-id="6ded0-144">Update hello configuration of hello specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="6ded0-145">Пример запроса</span><span class="sxs-lookup"><span data-stu-id="6ded0-145">Request example</span></span>

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

<span data-ttu-id="6ded0-146">значение Hello LoadBalancerDistribution может быть sourceIP для сходства двух кортежей, sourceIPProtocol сходства 3 кортежей или нет (для без сопоставления.</span><span class="sxs-lookup"><span data-stu-id="6ded0-146">hello value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="6ded0-147">т. е. балансировки по пяти кортежам).</span><span class="sxs-lookup"><span data-stu-id="6ded0-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="6ded0-148">Ответ</span><span class="sxs-lookup"><span data-stu-id="6ded0-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="6ded0-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6ded0-149">Next Steps</span></span>

[<span data-ttu-id="6ded0-150">Обзор внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="6ded0-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="6ded0-151">Приступая к настройке подсистемы балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="6ded0-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="6ded0-152">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="6ded0-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
