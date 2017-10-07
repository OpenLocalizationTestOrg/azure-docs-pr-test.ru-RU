---
title: "время ожидания простоя TCP подсистемы балансировки нагрузки aaaConfigure | Документы Microsoft"
description: "Описывается настройка времени ожидания простоя TCP для балансировщика нагрузки."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 4625c6a8-5725-47ce-81db-4fa3bd055891
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2bf0704b891f708e0a5bd7aa827441930f51cfaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="7de92-103">Настройка параметров времени ожидания простоя TCP для Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="7de92-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="7de92-104">В конфигурации по умолчанию значение параметра времени ожидания простоя для балансировщика нагрузки Azure равно 4 минутам.</span><span class="sxs-lookup"><span data-stu-id="7de92-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="7de92-105">Если периода бездействия превышает значение времени ожидания hello, нет никакой гарантии, что hello TCP или HTTP-сеанса сохраняется между hello клиентом и облачной службы.</span><span class="sxs-lookup"><span data-stu-id="7de92-105">If a period of inactivity is longer than hello timeout value, there's no guarantee that hello TCP or HTTP session is maintained between hello client and your cloud service.</span></span>

<span data-ttu-id="7de92-106">При закрытии соединения hello клиентское приложение может получить hello следующие сообщение об ошибке: «hello Базовое соединение закрыто: соединения, которое должно было находиться в активном состоянии toobe был закрыт сервером hello.»</span><span class="sxs-lookup"><span data-stu-id="7de92-106">When hello connection is closed, your client application may receive hello following error message: "hello underlying connection was closed: A connection that was expected toobe kept alive was closed by hello server."</span></span>

<span data-ttu-id="7de92-107">Распространенной практикой является toouse поддержание активности TCP.</span><span class="sxs-lookup"><span data-stu-id="7de92-107">A common practice is toouse a TCP keep-alive.</span></span> <span data-ttu-id="7de92-108">Такой подход делает активного подключения hello за более длительный период.</span><span class="sxs-lookup"><span data-stu-id="7de92-108">This practice keeps hello connection active for a longer period.</span></span> <span data-ttu-id="7de92-109">Дополнительные сведения вы найдете в следующих [примерах для .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="7de92-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="7de92-110">С активности включен, пакеты отправляются во время простоя в соединении hello.</span><span class="sxs-lookup"><span data-stu-id="7de92-110">With keep-alive enabled, packets are sent during periods of inactivity on hello connection.</span></span> <span data-ttu-id="7de92-111">Эти пакеты проверки активности убедитесь, что никогда не будет достигнуто значение тайм-аут простоя hello и hello подключение сохраняется в течение длительного периода.</span><span class="sxs-lookup"><span data-stu-id="7de92-111">These keep-alive packets ensure that hello idle timeout value is never reached and hello connection is maintained for a long period.</span></span>

<span data-ttu-id="7de92-112">Этот параметр действует только для входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="7de92-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="7de92-113">tooavoid проигравшей hello подключение, необходимо настроить hello поддержание активности TCP с интервалом меньше, чем hello тайм-аут простоя параметр или увеличьте hello значение времени ожидания простоя.</span><span class="sxs-lookup"><span data-stu-id="7de92-113">tooavoid losing hello connection, you must configure hello TCP keep-alive with an interval less than hello idle timeout setting or increase hello idle timeout value.</span></span> <span data-ttu-id="7de92-114">toosupport таких сценариев, мы добавили поддержку можно настроить время ожидания простоя.</span><span class="sxs-lookup"><span data-stu-id="7de92-114">toosupport such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="7de92-115">Теперь можно задать его в течение 4 минуты too30.</span><span class="sxs-lookup"><span data-stu-id="7de92-115">You can now set it for a duration of 4 too30 minutes.</span></span>

<span data-ttu-id="7de92-116">Проверки активности TCP хорошо подходят для сценариев, в которых нет ограничений, обусловленных временем работы аккумулятора.</span><span class="sxs-lookup"><span data-stu-id="7de92-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="7de92-117">Не рекомендуется для мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="7de92-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="7de92-118">С помощью поддержание активности TCP мобильного приложения могут выполнить сток батареи устройства hello быстрее.</span><span class="sxs-lookup"><span data-stu-id="7de92-118">Using a TCP keep-alive in a mobile application can drain hello device battery faster.</span></span>

![Время ожидания TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="7de92-120">Hello в следующих разделах описано, как toochange простоя параметры времени ожидания в виртуальных машин и облачных служб.</span><span class="sxs-lookup"><span data-stu-id="7de92-120">hello following sections describe how toochange idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a><span data-ttu-id="7de92-121">Настройка времени ожидания TCP hello на уровне экземпляра открытый IP too15 минут</span><span class="sxs-lookup"><span data-stu-id="7de92-121">Configure hello TCP timeout for your instance-level public IP too15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="7de92-122">`IdleTimeoutInMinutes` является необязательным.</span><span class="sxs-lookup"><span data-stu-id="7de92-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="7de92-123">Если не задано, время ожидания по умолчанию hello составляет 4 минуты.</span><span class="sxs-lookup"><span data-stu-id="7de92-123">If it is not set, hello default timeout is 4 minutes.</span></span> <span data-ttu-id="7de92-124">диапазон Hello допустимое время ожидания составляет 4 минуты too30.</span><span class="sxs-lookup"><span data-stu-id="7de92-124">hello acceptable timeout range is 4 too30 minutes.</span></span>

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="7de92-125">Задать время ожидания простоя hello при создании конечной точки Azure на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="7de92-125">Set hello idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="7de92-126">toochange Здравствуйте времени ожидания для конечной точки, используйте hello ниже:</span><span class="sxs-lookup"><span data-stu-id="7de92-126">toochange hello timeout setting for an endpoint, use hello following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="7de92-127">tooretrieve конфигурацию тайм-аут простоя hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7de92-127">tooretrieve your idle timeout configuration, use hello following command:</span></span>

    PS C:\> Get-AzureVM -ServiceName "MyService" -Name "MyVM" | Get-AzureEndpoint
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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="7de92-128">Задать время ожидания TCP hello на набор конечных точек с балансировкой нагрузки</span><span class="sxs-lookup"><span data-stu-id="7de92-128">Set hello TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="7de92-129">Если конечные точки являются частью набора конечных точек с балансировкой нагрузки, времени ожидания TCP hello должно задаваться на набор конечных точек с балансировкой нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="7de92-129">If endpoints are part of a load-balanced endpoint set, hello TCP timeout must be set on hello load-balanced endpoint set.</span></span> <span data-ttu-id="7de92-130">Например:</span><span class="sxs-lookup"><span data-stu-id="7de92-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="7de92-131">Изменение параметров времени ожидания для облачных служб</span><span class="sxs-lookup"><span data-stu-id="7de92-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="7de92-132">Можно использовать tooupdate hello Azure SDK облачной службы.</span><span class="sxs-lookup"><span data-stu-id="7de92-132">You can use hello Azure SDK tooupdate your cloud service.</span></span> <span data-ttu-id="7de92-133">Параметры конечной точки для облачных служб, внесенные в файл csdef hello.</span><span class="sxs-lookup"><span data-stu-id="7de92-133">You make endpoint settings for cloud services in hello .csdef file.</span></span> <span data-ttu-id="7de92-134">При обновлении hello времени ожидания TCP для развертывания облачной службы требуется обновление развертывания.</span><span class="sxs-lookup"><span data-stu-id="7de92-134">Updating hello TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="7de92-135">Исключение, если время ожидания TCP hello указывается только для общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="7de92-135">An exception is if hello TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="7de92-136">Открытые параметры IP-адреса находятся в файле .cscfg hello и их можно было обновить до обновления развертывания и обновления.</span><span class="sxs-lookup"><span data-stu-id="7de92-136">Public IP settings are in hello .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="7de92-137">присутствуют изменения .csdef Hello для настройки конечной точки:</span><span class="sxs-lookup"><span data-stu-id="7de92-137">hello .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="7de92-138">присутствуют изменения .cscfg Hello hello параметра времени ожидания на общедоступных IP-адресов:</span><span class="sxs-lookup"><span data-stu-id="7de92-138">hello .cscfg changes for hello timeout setting on public IPs are:</span></span>

```xml
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

## <a name="rest-api-example"></a><span data-ttu-id="7de92-139">Пример для REST API</span><span class="sxs-lookup"><span data-stu-id="7de92-139">REST API example</span></span>

<span data-ttu-id="7de92-140">Время ожидания простоя TCP hello можно настроить с помощью API управления службами hello.</span><span class="sxs-lookup"><span data-stu-id="7de92-140">You can configure hello TCP idle timeout by using hello service management API.</span></span> <span data-ttu-id="7de92-141">Убедитесь в том, что hello `x-ms-version` задан заголовок tooversion `2014-06-01` или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7de92-141">Make sure that hello `x-ms-version` header is set tooversion `2014-06-01` or later.</span></span> <span data-ttu-id="7de92-142">Обновление конфигурации hello hello указанные входных конечных точек с балансировкой нагрузки на все виртуальные машины в развертывании.</span><span class="sxs-lookup"><span data-stu-id="7de92-142">Update hello configuration of hello specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="7de92-143">Запрос</span><span class="sxs-lookup"><span data-stu-id="7de92-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="7de92-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="7de92-144">Response</span></span>

```xml
<LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <InputEndpoint>
    <LoadBalancedEndpointSetName>endpoint-set-name</LoadBalancedEndpointSetName>
    <LocalPort>local-port-number</LocalPort>
    <Port>external-port-number</Port>
    <LoadBalancerProbe>
        <Path>path-of-probe</Path>
        <Port>port-assigned-to-probe</Port>
        <Protocol>probe-protocol</Protocol>
        <IntervalInSeconds>interval-of-probe</IntervalInSeconds>
        <TimeoutInSeconds>timeout-for-probe</TimeoutInSeconds>
    </LoadBalancerProbe>
    <LoadBalancerName>name-of-internal-loadbalancer</LoadBalancerName>
    <Protocol>endpoint-protocol</Protocol>
    <IdleTimeoutInMinutes>15</IdleTimeoutInMinutes>
    <EnableDirectServerReturn>enable-direct-server-return</EnableDirectServerReturn>
    <EndpointACL>
        <Rules>
        <Rule>
            <Order>priority-of-the-rule</Order>
            <Action>permit-rule</Action>
            <RemoteSubnet>subnet-of-the-rule</RemoteSubnet>
            <Description>description-of-the-rule</Description>
        </Rule>
        </Rules>
    </EndpointACL>
    </InputEndpoint>
</LoadBalancedEndpointList>
```

## <a name="next-steps"></a><span data-ttu-id="7de92-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7de92-145">Next steps</span></span>

[<span data-ttu-id="7de92-146">Обзор внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="7de92-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="7de92-147">Приступая к настройке балансировщика нагрузки для Интернета</span><span class="sxs-lookup"><span data-stu-id="7de92-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="7de92-148">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="7de92-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
