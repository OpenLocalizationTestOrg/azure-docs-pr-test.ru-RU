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
# <a name="configure-hello-distribution-mode-for-load-balancer"></a>Настройка режима hello распространения для подсистемы балансировки нагрузки

## <a name="hash-based-distribution-mode"></a>Режим распространения на основе хэша

алгоритм распределения Hello по умолчанию — 5-фрагментному (исходный IP-адрес, порт источника тип протокола конечный IP-адрес, порт назначения) хэш-серверы tooavailable toomap трафика. Он позволяет закреплять IP-адреса только в рамках сеанса транспорта. Пакетов в hello того же сеанса, будут направляться toohello экземпляра центра обработки данных IP-адрес (DIP) за конечной точкой с балансировкой нагрузки hello. При запуске клиента hello новый сеанс из Здравствуйте же исходный IP-адрес, порт источника hello изменяется в результате чего hello трафика toogo tooa другой DIP-адрес конечной точки.

![подсистема балансировки нагрузки на основе хэша](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

Рис. 1. Пятикортежное распределение

## <a name="source-ip-affinity-mode"></a>Режим сходства исходного IP-адреса

Доступен новый режим распределения — соответствие исходному IP-адресу (также известный как соответствие сеансу или соответствие клиентскому IP-адресу). Подсистема балансировки нагрузки Azure может быть настроенный toouse кортеж из двух (исходный IP-адрес, конечный IP-адрес) или toomap (исходный IP-адрес, конечный IP-адрес, протокол) кортежа трафика toohello доступных серверов. С помощью сходства исходный IP-адрес, подключений инициированный hello же клиентский компьютер проходит toohello DIP-адрес конечной точки.

Следующая схема Hello показана конфигурация двух кортежей. Обратите внимание на то, как кортеж hello завершит hello нагрузки балансировки toovirtual машины 1 (VM1) которого затем резервной копии, созданной VM2 и VM3.

![Сходство сеансов](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

Рис. 2. Двухкортежное распределение

Сопоставление источника IP решает несовместимости hello подсистемы балансировки нагрузки Azure и шлюза удаленных рабочих столов (RD). Теперь можно создать ферму шлюза удаленных рабочих столов в одной облачной службе.

Другой вариант сценария использования — передача мультимедиа, где hello передача данных происходит через UDP, но hello плоскости управления достигается с помощью TCP:

* Клиент инициирует сеанс TCP с балансировкой нагрузки toohello общедоступный адрес, сначала возвращает расширенный tooa конкретных DIP, этот канал является работоспособность подключения левой active toomonitor hello
* Новый сеанс UDP из hello же клиент запустил toohello общедоступную конечную точку с балансировкой нагрузки на одном, hello здесь ожидается этого подключения также является направленным toohello DIP-адрес конечной точки предыдущего TCP-соединение hello, чтобы передать носитель может быть выполнен на высокую пропускную способность, сохраняя канал управления через TCP.

> [!NOTE]
> При изменении набора с балансировкой нагрузки (или удалении виртуальной машины) будет пересчитано hello распределения запросов клиентов. Не следует рассчитывать новые соединения из существующих клиентов, попадающих в hello же сервера. Кроме того, использование режима распределения соответствия исходному IP-адресу может привести к неравномерному распределению трафика. Клиенты, работающие на прокси-серверах, могут рассматриваться как одно уникальное клиентское приложение.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>Настройка параметров соответствия исходному IP-адресу для подсистемы балансировки нагрузки

Для виртуальных машин можно использовать параметры времени ожидания toochange PowerShell:

Добавление конечной точки Azure tooa виртуальную машину и установите режим распространения подсистемы балансировки нагрузки

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

LoadBalancerDistribution можно задать toosourceIP для двух кортежей (исходный IP-адрес, конечный IP-адрес), балансировка нагрузки sourceIPProtocol для балансировки нагрузки (исходный IP-адрес, конечный IP-адрес, протокол) кортежа или none, если необходимо поведение по умолчанию hello 5-фрагментному балансировки нагрузки.

Используйте следующие tooretrieve конфигурации конечной точки распространения подсистемы балансировки нагрузки режим hello.

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

Если отсутствует элемент LoadBalancerDistribution hello hello балансировки нагрузки Azure использует алгоритм 5-фрагментному по умолчанию hello.

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a>Установить режим распространения hello для набора конечных точек с балансировкой нагрузки

Если конечные точки являются частью набора конечных точек с балансировкой нагрузки, режим распространения hello необходимо установить на набор конечных точек с балансировкой нагрузки hello.

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a>Облачные службы конфигурации toochange распространения режим

Вы можете использовать hello Azure SDK для .NET 2.5 (toobe выпущенных в ноябре) tooupdate облачной службы. Параметры конечной точки для облачных служб, выполняемых в hello .csdef. В порядке tooupdate hello балансировки режим распределения нагрузки развертывания облачных служб требуется обновление развертывания.
Ниже приведен пример изменений в CSDEF-файле для настройки конечных точек:

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

## <a name="api-example"></a>Пример API

Вы можете настроить распространение подсистемы балансировки нагрузки hello, с помощью API управления службами hello. Убедитесь, что hello tooadd `x-ms-version` задан заголовок tooversion `2014-09-01` или более поздней версии.

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a>Обновление конфигурации hello hello указан набор балансировки нагрузки в развертывании

#### <a name="request-example"></a>Пример запроса

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

значение Hello LoadBalancerDistribution может быть sourceIP для сходства двух кортежей, sourceIPProtocol сходства 3 кортежей или нет (для без сопоставления. т. е. балансировки по пяти кортежам).

#### <a name="response"></a>Ответ

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a>Дальнейшие действия

[Обзор внутренней подсистемы балансировки нагрузки](load-balancer-internal-overview.md)

[Приступая к настройке подсистемы балансировки нагрузки, доступной в Интернете](load-balancer-get-started-internet-arm-ps.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)
