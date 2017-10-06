---
title: "aaaCreate внутренний загрузить балансировки - Azure CLI классический | Документы Microsoft"
description: "Узнайте, как toocreate балансировщик внутренней нагрузки с помощью hello Azure CLI в hello классической модели развертывания"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a>Приступая к созданию внутренней подсистемы балансировки нагрузки (классической) с помощью hello Azure CLI

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Облачные службы](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).  В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](load-balancer-get-started-ilb-arm-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a>toocreate внутренний балансировщик нагрузки для виртуальных машин

toocreate внутренний балансировщик нагрузки задать и hello серверов, которые будут отправлять их tooit трафика, необходимо выполнить следующие hello:

1. Создайте экземпляр внутренней балансировки нагрузки, конечную точку hello входящего трафика toobe Балансировка нагрузки для серверов hello набора балансировки нагрузки.
2. Добавьте конечные точки, соответствующие toohello виртуальных машин, которые будут принимать входящий трафик hello.
3. Настройка серверов hello, которые будут отправлять что hello трафика toobe с балансировкой нагрузки toosend их трафика toohello виртуальных IP-адресов (VIP) адрес экземпляра hello внутренней балансировки.

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a>Пошаговая процедура создания внутреннего балансировщика нагрузки с помощью интерфейса командной строки

В этом руководстве показано, как toocreate внутренний балансировщик нагрузки на основе hello сценарии выше.

1. Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.
2. Запустите hello **azure конфигурации режима** режим tooclassic команд tooswitch, как показано ниже.

    ```azurecli
    azure config mode asm
    ```

    Ожидаемые выходные данные:

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Создание набора балансировщика нагрузки и конечной точки

Hello сценарий предполагает hello виртуальные машины «DB1» и «DB2» в облачной службе, называется «mytestcloud». Обе виртуальные машины используют виртуальную сеть с именем "testvnet" с подсетью "subnet-1".

В этом руководстве будет создан набор внутренних балансировщиков нагрузки с использованием порта 1433 в качестве частного порта и порта 1433 в качестве локального порта.

Это общие сценарии, где имеется SQL виртуальных машин на hello серверной части, используя внутренней нагрузки серверов балансировки tooguarantee hello базы данных не будет предоставляться напрямую, используя общедоступный IP-адрес.

### <a name="step-1"></a>Шаг 1

Создайте набор внутренних балансировщиков нагрузки с помощью `azure network service internal-load-balancer add`.

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

Дополнительные сведения см. в `azure service internal-load-balancer --help`.

Вы можете проверить hello свойства внутреннего балансировщика нагрузки с помощью команды hello `azure service internal-load-balancer list` *имя облачной службы*.

Здесь пример hello выходных данных выглядит следующим образом:

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a>Шаг 2

Настройки hello внутренней подсистемы балансировки нагрузки задается при добавлении hello первую конечную точку. Будет связывать hello конечной точки, виртуальной машины и проверки порт toohello внутренний набор балансировщиков нагрузки на этом шаге.

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a>Шаг 3.

Проверьте hello нагрузки балансировки конфигурации с помощью `azure vm show` *имя виртуальной машины*

```azurecli
azure vm show DB1
```

Hello выходные данные будут:

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Создание конечной точки удаленного рабочего стола для виртуальной машины

Вы можете создать удаленного рабочего стола конечной точки tooforward сетевого трафика на локальный порт tooa открытый порт для конкретной виртуальной машины с помощью `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Удаление виртуальной машины из балансировщика нагрузки

Можно удалить виртуальную машину из внутренний набор балансировщиков нагрузки путем удаления связанных hello конечной точки. После удаления конечной точки hello hello виртуальной машины не принадлежит набор больше toohello с балансировкой нагрузки.

С помощью приведенном выше примере hello, можно удалить hello конечной точки, созданной для виртуальной машины «DB1» из внутренней подсистемы балансировки нагрузки «ilbset» с помощью команды hello `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

Дополнительные сведения см. в `azure vm endpoint --help`.

## <a name="next-steps"></a>Дальнейшие действия

[Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)
