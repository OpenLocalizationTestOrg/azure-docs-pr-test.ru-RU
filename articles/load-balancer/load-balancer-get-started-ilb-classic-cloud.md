---
title: "Внутренняя Подсистема балансировки нагрузки для облачных служб Azure aaaCreate | Документы Microsoft"
description: "Узнайте, как с помощью PowerShell в hello классической модели развертывания подсистемы балансировки нагрузки, toocreate во внутренний"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>Начало работы по созданию внутреннего балансировщика нагрузки (классическая версия) для облачных служб

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Облачные службы](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).  В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](load-balancer-get-started-ilb-arm-ps.md).

## <a name="configure-internal-load-balancer-for-cloud-services"></a>Настройка внутреннего балансировщика нагрузки для облачных служб

Внутренний балансировщик нагрузки поддерживается как для виртуальных машин, так и для облачных служб. Внутренняя нагрузки балансировки конечной точки, созданной в облачной службе, который находится за пределами региональной виртуальной сети будут доступны только в пределах hello облачной службы.

конфигурация подсистемы балансировки нагрузки внутренней Hello имеет toobe задать во время создания hello hello первого развертывания в облачной службе hello, как показано в следующем примере hello.

> [!IMPORTANT]
> Следующие действия hello готовности toorun — toohave виртуальная сеть уже создан для развертывания облака hello. Вам потребуется hello виртуального сетевого имени и подсети имя toocreate hello внутренней балансировки нагрузки.

### <a name="step-1"></a>Шаг 1

Откройте hello файла конфигурации службы (csfg) для развертывания облака в Visual Studio и добавьте следующий раздел toocreate hello внутренней балансировки нагрузки в группе hello последнего hello "`</Role>`" элемента конфигурации сети hello.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Давайте добавим hello значения для hello конфигурации сети файла tooshow, как будет выглядеть. В примере hello предполагается, что вы создали виртуальную сеть, называется «test_vnet» с подсети 10.0.0.0/24 test_subnet и статический IP-адрес 10.0.0.4. Подсистема балансировки нагрузки Hello будет называться testLB.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Дополнительные сведения о схеме подсистемы балансировки нагрузки hello см. в разделе [балансировки нагрузки добавить](https://msdn.microsoft.com/library/azure/dn722411.aspx).

### <a name="step-2"></a>Шаг 2

Изменение конечных точек hello службы определения службы(.csdef) файл tooadd toohello с внутренней балансировки нагрузки. Hello момент создания экземпляра роли, добавляет файл определения службы hello hello роль экземпляров toohello внутренняя Балансировка нагрузки.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

Следующие hello же значения в приведенном выше примере hello добавим файл определения службы toohello значения hello.

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

Hello сетевой трафик будет с помощью подсистемы балансировки нагрузки hello testLB использовать порт 80 для входящих запросов, отправка tooworker экземпляры роли также через порт 80 с балансировкой нагрузки.

## <a name="next-steps"></a>Дальнейшие действия

[Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)

