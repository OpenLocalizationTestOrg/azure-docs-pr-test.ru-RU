---
title: "Настройка времени ожидания простоя TCP для балансировщика нагрузки | Документация Майкрософт"
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
ms.openlocfilehash: d040fe6580b8ae777aecc9dd385ed33861530c38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="ea94e-103">Настройка параметров времени ожидания простоя TCP для Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="ea94e-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="ea94e-104">В конфигурации по умолчанию значение параметра времени ожидания простоя для балансировщика нагрузки Azure равно 4 минутам.</span><span class="sxs-lookup"><span data-stu-id="ea94e-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="ea94e-105">Если период бездействия превышает значение времени ожидания, нет никакой гарантии, что сеанс TCP или HTTP между клиентом и облачной службой возобновится.</span><span class="sxs-lookup"><span data-stu-id="ea94e-105">If a period of inactivity is longer than the timeout value, there's no guarantee that the TCP or HTTP session is maintained between the client and your cloud service.</span></span>

<span data-ttu-id="ea94e-106">При закрытии подключения клиентское приложение может получить такое сообщение об ошибке: "Базовое соединение закрыто. Соединение, которое должно было работать, было разорвано сервером".</span><span class="sxs-lookup"><span data-stu-id="ea94e-106">When the connection is closed, your client application may receive the following error message: "The underlying connection was closed: A connection that was expected to be kept alive was closed by the server."</span></span>

<span data-ttu-id="ea94e-107">Распространенной практикой является проверка активности TCP.</span><span class="sxs-lookup"><span data-stu-id="ea94e-107">A common practice is to use a TCP keep-alive.</span></span> <span data-ttu-id="ea94e-108">Такой подход позволяет поддерживать подключения активными в течение более длительного периода.</span><span class="sxs-lookup"><span data-stu-id="ea94e-108">This practice keeps the connection active for a longer period.</span></span> <span data-ttu-id="ea94e-109">Дополнительные сведения вы найдете в следующих [примерах для .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea94e-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="ea94e-110">Когда проверка активности включена, пакеты отправляются в периоды простоя подключений.</span><span class="sxs-lookup"><span data-stu-id="ea94e-110">With keep-alive enabled, packets are sent during periods of inactivity on the connection.</span></span> <span data-ttu-id="ea94e-111">Благодаря пакетам проверки активности значение времени ожидания простоя не достигается и подключение сохраняется в течение длительного времени.</span><span class="sxs-lookup"><span data-stu-id="ea94e-111">These keep-alive packets ensure that the idle timeout value is never reached and the connection is maintained for a long period.</span></span>

<span data-ttu-id="ea94e-112">Этот параметр действует только для входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="ea94e-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="ea94e-113">Чтобы избежать потери подключения, необходимо настроить проверку активности TCP с интервалом, который должен быть меньше, чем время ожидания простоя. Можно также увеличить значение времени ожидания простоя.</span><span class="sxs-lookup"><span data-stu-id="ea94e-113">To avoid losing the connection, you must configure the TCP keep-alive with an interval less than the idle timeout setting or increase the idle timeout value.</span></span> <span data-ttu-id="ea94e-114">Для поддержки таких сценариев мы добавили возможность настройки времени ожидания простоя.</span><span class="sxs-lookup"><span data-stu-id="ea94e-114">To support such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="ea94e-115">Теперь для него можно задать значение от 4 до 30 минут.</span><span class="sxs-lookup"><span data-stu-id="ea94e-115">You can now set it for a duration of 4 to 30 minutes.</span></span>

<span data-ttu-id="ea94e-116">Проверки активности TCP хорошо подходят для сценариев, в которых нет ограничений, обусловленных временем работы аккумулятора.</span><span class="sxs-lookup"><span data-stu-id="ea94e-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="ea94e-117">Не рекомендуется для мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="ea94e-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="ea94e-118">Использование этого метода в мобильном приложении может привести к ускоренной разрядке аккумулятора устройства.</span><span class="sxs-lookup"><span data-stu-id="ea94e-118">Using a TCP keep-alive in a mobile application can drain the device battery faster.</span></span>

![Время ожидания TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="ea94e-120">В приведенных ниже разделах описывается, как изменить параметры времени ожидания простоя в виртуальных машинах и облачных службах.</span><span class="sxs-lookup"><span data-stu-id="ea94e-120">The following sections describe how to change idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-the-tcp-timeout-for-your-instance-level-public-ip-to-15-minutes"></a><span data-ttu-id="ea94e-121">Настройка для времени ожидания TCP, равного 15 минутам, для общедоступного IP-адреса уровня экземпляра</span><span class="sxs-lookup"><span data-stu-id="ea94e-121">Configure the TCP timeout for your instance-level public IP to 15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="ea94e-122">`IdleTimeoutInMinutes` является необязательным.</span><span class="sxs-lookup"><span data-stu-id="ea94e-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="ea94e-123">Если значение параметра не задано, время ожидания по умолчанию будет составлять 4 минуты.</span><span class="sxs-lookup"><span data-stu-id="ea94e-123">If it is not set, the default timeout is 4 minutes.</span></span> <span data-ttu-id="ea94e-124">Допустимый диапазон времени ожидания — от 4 до 30 минут.</span><span class="sxs-lookup"><span data-stu-id="ea94e-124">The acceptable timeout range is 4 to 30 minutes.</span></span>

## <a name="set-the-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="ea94e-125">Настройка времени ожидания простоя при создании конечной точки Azure в виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="ea94e-125">Set the idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="ea94e-126">Чтобы изменить параметр времени ожидания для конечной точки, используйте следующее:</span><span class="sxs-lookup"><span data-stu-id="ea94e-126">To change the timeout setting for an endpoint, use the following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="ea94e-127">Чтобы получить конфигурацию времени ожидания простоя, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ea94e-127">To retrieve your idle timeout configuration, use the following command:</span></span>

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

## <a name="set-the-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="ea94e-128">Настройка времени ожидания TCP для набора конечных точек с балансировкой нагрузки</span><span class="sxs-lookup"><span data-stu-id="ea94e-128">Set the TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="ea94e-129">Если набор балансировки нагрузки для конечных точек содержит конечные точки, для него следует установить время ожидания TCP.</span><span class="sxs-lookup"><span data-stu-id="ea94e-129">If endpoints are part of a load-balanced endpoint set, the TCP timeout must be set on the load-balanced endpoint set.</span></span> <span data-ttu-id="ea94e-130">Например:</span><span class="sxs-lookup"><span data-stu-id="ea94e-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="ea94e-131">Изменение параметров времени ожидания для облачных служб</span><span class="sxs-lookup"><span data-stu-id="ea94e-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="ea94e-132">Вы можете обновить облачную службу с помощью пакета Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="ea94e-132">You can use the Azure SDK to update your cloud service.</span></span> <span data-ttu-id="ea94e-133">Параметры конечных точек для облачных служб можно настроить в CSDEF-файле.</span><span class="sxs-lookup"><span data-stu-id="ea94e-133">You make endpoint settings for cloud services in the .csdef file.</span></span> <span data-ttu-id="ea94e-134">Чтобы обновить время ожидания TCP для развертывания облачной службы, требуется обновить развертывание.</span><span class="sxs-lookup"><span data-stu-id="ea94e-134">Updating the TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="ea94e-135">Исключением является случай, когда время ожидания TCP задано только для общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="ea94e-135">An exception is if the TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="ea94e-136">Параметры общедоступного IP-адреса находятся в CSCFG-файле, и их можно обновить в процессе обновления развертывания и установки новой версии.</span><span class="sxs-lookup"><span data-stu-id="ea94e-136">Public IP settings are in the .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="ea94e-137">Ниже перечислены изменения в настройках конечной точки в CSCFG-файле:</span><span class="sxs-lookup"><span data-stu-id="ea94e-137">The .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="ea94e-138">Изменения CSCFG-файла для параметров времени ожидания общедоступных IP-адресов приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="ea94e-138">The .cscfg changes for the timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="ea94e-139">Пример для REST API</span><span class="sxs-lookup"><span data-stu-id="ea94e-139">REST API example</span></span>

<span data-ttu-id="ea94e-140">Можно настроить время ожидания простоя TCP с помощью API управления службами.</span><span class="sxs-lookup"><span data-stu-id="ea94e-140">You can configure the TCP idle timeout by using the service management API.</span></span> <span data-ttu-id="ea94e-141">Убедитесь, что для заголовка `x-ms-version` задана версия `2014-06-01` или более поздняя.</span><span class="sxs-lookup"><span data-stu-id="ea94e-141">Make sure that the `x-ms-version` header is set to version `2014-06-01` or later.</span></span> <span data-ttu-id="ea94e-142">Обновите конфигурацию указанных конечных точек ввода с балансировкой нагрузки для всех виртуальных машин в развертывании.</span><span class="sxs-lookup"><span data-stu-id="ea94e-142">Update the configuration of the specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="ea94e-143">Запрос</span><span class="sxs-lookup"><span data-stu-id="ea94e-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="ea94e-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="ea94e-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ea94e-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ea94e-145">Next steps</span></span>

[<span data-ttu-id="ea94e-146">Обзор внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="ea94e-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="ea94e-147">Приступая к настройке балансировщика нагрузки для Интернета</span><span class="sxs-lookup"><span data-stu-id="ea94e-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="ea94e-148">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="ea94e-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
