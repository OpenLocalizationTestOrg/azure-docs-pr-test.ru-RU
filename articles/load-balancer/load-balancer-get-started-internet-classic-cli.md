---
title: "Подсистема балансировки - нагрузки на aaaCreate из Интернета, Azure CLI классический | Документы Microsoft"
description: "Узнайте, как toocreate с выходом подсистемы балансировки нагрузки Интернета в классическом развертывании модели с помощью hello Azure CLI"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a>Приступая к созданию подсистемы балансировки нагрузки (классические) в hello Azure CLI с выходом в Интернет

> [!div class="op_single_selector"]
> * [классическом портале Azure](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [облачных служб Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчера ресурсов Azure и классическом. Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure. Для просмотра документации hello для различных средств, щелкнув вкладки hello hello верхней части этой статьи. В этой статье рассматриваются hello классической модели развертывания. Вы также можете [Узнайте, как с помощью диспетчера ресурсов Azure подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a>Пошаговая процедура создания балансировщика нагрузки для Интернета с помощью интерфейса командной строки

В этом руководстве показано, как toocreate Internet балансировки нагрузки на основе hello сценарии выше.

1. Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.
2. Запустите hello **azure конфигурации режима** режим tooclassic команд tooswitch, как показано ниже.

    ```azurecli
    azure config mode asm
    ```

    Ожидаемые выходные данные:

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Создание набора балансировщика нагрузки и конечной точки

Hello сценарий предполагает hello виртуальных машин «web1» и «web2» были созданы.
В этом руководстве будет создан набор балансировщика нагрузки с использованием общего порта 80 и локального порта 80. Порт пробы настроен на порт 80 и балансировки нагрузки hello именованный набор «набор балансировки нагрузки».

### <a name="step-1"></a>Шаг 1

Создайте конечную точку hello для первой и задать с помощью подсистемы балансировки нагрузки `azure network vm endpoint create` для виртуальной машины «web1».

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a>Шаг 2

Добавьте второй набор балансировки нагрузки виртуальной машины «web2» toohello.

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a>Шаг 3.

Проверьте hello нагрузки балансировки конфигурации с помощью `azure vm show` .

```azurecli
azure vm show web1
```

Hello выходные данные будут:

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Создание конечной точки удаленного рабочего стола для виртуальной машины

Вы можете создать удаленного рабочего стола конечной точки tooforward сетевого трафика на локальный порт tooa открытый порт для конкретной виртуальной машины с помощью `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Удаление виртуальной машины из балансировщика нагрузки

У вас есть toodelete hello конечная точка, связанная toohello набору балансировки нагрузки из hello виртуальной машины. После удаления конечной точки hello hello виртуальной машины не принадлежит набор больше toohello с балансировкой нагрузки.

Используя пример hello выше, можно удалить hello конечной точки, созданной для виртуальной машины «web1» из балансировки нагрузки набор балансировки» нагрузки» с помощью команды hello `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> Вы можете просматривать параметры toomanage конечных точек с помощью команды hello`azure vm endpoint --help`

## <a name="next-steps"></a>Дальнейшие действия

[Приступая к настройке внутренней подсистемы балансировки нагрузки](load-balancer-get-started-ilb-arm-ps.md)

[Настройка режима распределения подсистемы балансировки нагрузки](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)
