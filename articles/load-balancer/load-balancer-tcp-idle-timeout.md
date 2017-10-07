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
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a>Настройка параметров времени ожидания простоя TCP для Azure Load Balancer

В конфигурации по умолчанию значение параметра времени ожидания простоя для балансировщика нагрузки Azure равно 4 минутам. Если периода бездействия превышает значение времени ожидания hello, нет никакой гарантии, что hello TCP или HTTP-сеанса сохраняется между hello клиентом и облачной службы.

При закрытии соединения hello клиентское приложение может получить hello следующие сообщение об ошибке: «hello Базовое соединение закрыто: соединения, которое должно было находиться в активном состоянии toobe был закрыт сервером hello.»

Распространенной практикой является toouse поддержание активности TCP. Такой подход делает активного подключения hello за более длительный период. Дополнительные сведения вы найдете в следующих [примерах для .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx). С активности включен, пакеты отправляются во время простоя в соединении hello. Эти пакеты проверки активности убедитесь, что никогда не будет достигнуто значение тайм-аут простоя hello и hello подключение сохраняется в течение длительного периода.

Этот параметр действует только для входящих подключений. tooavoid проигравшей hello подключение, необходимо настроить hello поддержание активности TCP с интервалом меньше, чем hello тайм-аут простоя параметр или увеличьте hello значение времени ожидания простоя. toosupport таких сценариев, мы добавили поддержку можно настроить время ожидания простоя. Теперь можно задать его в течение 4 минуты too30.

Проверки активности TCP хорошо подходят для сценариев, в которых нет ограничений, обусловленных временем работы аккумулятора. Не рекомендуется для мобильных приложений. С помощью поддержание активности TCP мобильного приложения могут выполнить сток батареи устройства hello быстрее.

![Время ожидания TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

Hello в следующих разделах описано, как toochange простоя параметры времени ожидания в виртуальных машин и облачных служб.

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a>Настройка времени ожидания TCP hello на уровне экземпляра открытый IP too15 минут

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

`IdleTimeoutInMinutes` является необязательным. Если не задано, время ожидания по умолчанию hello составляет 4 минуты. диапазон Hello допустимое время ожидания составляет 4 минуты too30.

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a>Задать время ожидания простоя hello при создании конечной точки Azure на виртуальной машине

toochange Здравствуйте времени ожидания для конечной точки, используйте hello ниже:

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

tooretrieve конфигурацию тайм-аут простоя hello используйте следующую команду:

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a>Задать время ожидания TCP hello на набор конечных точек с балансировкой нагрузки

Если конечные точки являются частью набора конечных точек с балансировкой нагрузки, времени ожидания TCP hello должно задаваться на набор конечных точек с балансировкой нагрузки hello. Например:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a>Изменение параметров времени ожидания для облачных служб

Можно использовать tooupdate hello Azure SDK облачной службы. Параметры конечной точки для облачных служб, внесенные в файл csdef hello. При обновлении hello времени ожидания TCP для развертывания облачной службы требуется обновление развертывания. Исключение, если время ожидания TCP hello указывается только для общедоступного IP-адреса. Открытые параметры IP-адреса находятся в файле .cscfg hello и их можно было обновить до обновления развертывания и обновления.

присутствуют изменения .csdef Hello для настройки конечной точки:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

присутствуют изменения .cscfg Hello hello параметра времени ожидания на общедоступных IP-адресов:

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

## <a name="rest-api-example"></a>Пример для REST API

Время ожидания простоя TCP hello можно настроить с помощью API управления службами hello. Убедитесь в том, что hello `x-ms-version` задан заголовок tooversion `2014-06-01` или более поздней версии. Обновление конфигурации hello hello указанные входных конечных точек с балансировкой нагрузки на все виртуальные машины в развертывании.

### <a name="request"></a>Запрос

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a>Ответ

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

## <a name="next-steps"></a>Дальнейшие действия

[Обзор внутренней подсистемы балансировки нагрузки](load-balancer-internal-overview.md)

[Приступая к настройке балансировщика нагрузки для Интернета](load-balancer-get-started-internet-arm-ps.md)

[Настройка режима распределения подсистемы балансировки нагрузки](load-balancer-distribution-mode.md)
