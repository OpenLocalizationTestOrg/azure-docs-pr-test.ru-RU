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
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a><span data-ttu-id="fe1ea-103">Приступая к созданию подсистемы балансировки нагрузки (классические) в hello Azure CLI с выходом в Интернет</span><span class="sxs-lookup"><span data-stu-id="fe1ea-103">Get started creating an Internet facing load balancer (classic) in hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe1ea-104">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="fe1ea-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="fe1ea-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe1ea-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="fe1ea-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="fe1ea-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="fe1ea-107">облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="fe1ea-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="fe1ea-108">Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчера ресурсов Azure и классическом.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="fe1ea-109">Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="fe1ea-110">Для просмотра документации hello для различных средств, щелкнув вкладки hello hello верхней части этой статьи.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="fe1ea-111">В этой статье рассматриваются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="fe1ea-112">Вы также можете [Узнайте, как с помощью диспетчера ресурсов Azure подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fe1ea-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="fe1ea-113">Пошаговая процедура создания балансировщика нагрузки для Интернета с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="fe1ea-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="fe1ea-114">В этом руководстве показано, как toocreate Internet балансировки нагрузки на основе hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-114">This guide shows how toocreate an Internet load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="fe1ea-115">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-115">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="fe1ea-116">Запустите hello **azure конфигурации режима** режим tooclassic команд tooswitch, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-116">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="fe1ea-117">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fe1ea-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="fe1ea-118">Создание набора балансировщика нагрузки и конечной точки</span><span class="sxs-lookup"><span data-stu-id="fe1ea-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="fe1ea-119">Hello сценарий предполагает hello виртуальных машин «web1» и «web2» были созданы.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-119">hello scenario assumes hello virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="fe1ea-120">В этом руководстве будет создан набор балансировщика нагрузки с использованием общего порта 80 и локального порта 80.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="fe1ea-121">Порт пробы настроен на порт 80 и балансировки нагрузки hello именованный набор «набор балансировки нагрузки».</span><span class="sxs-lookup"><span data-stu-id="fe1ea-121">A probe port is also configured on port 80 and named hello load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="fe1ea-122">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="fe1ea-122">Step 1</span></span>

<span data-ttu-id="fe1ea-123">Создайте конечную точку hello для первой и задать с помощью подсистемы балансировки нагрузки `azure network vm endpoint create` для виртуальной машины «web1».</span><span class="sxs-lookup"><span data-stu-id="fe1ea-123">Create hello first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="fe1ea-124">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="fe1ea-124">Step 2</span></span>

<span data-ttu-id="fe1ea-125">Добавьте второй набор балансировки нагрузки виртуальной машины «web2» toohello.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-125">Add a second virtual machine "web2" toohello load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="fe1ea-126">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-126">Step 3</span></span>

<span data-ttu-id="fe1ea-127">Проверьте hello нагрузки балансировки конфигурации с помощью `azure vm show` .</span><span class="sxs-lookup"><span data-stu-id="fe1ea-127">Verify hello load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="fe1ea-128">Hello выходные данные будут:</span><span class="sxs-lookup"><span data-stu-id="fe1ea-128">hello output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="fe1ea-129">Создание конечной точки удаленного рабочего стола для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="fe1ea-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="fe1ea-130">Вы можете создать удаленного рабочего стола конечной точки tooforward сетевого трафика на локальный порт tooa открытый порт для конкретной виртуальной машины с помощью `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-130">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="fe1ea-131">Удаление виртуальной машины из балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="fe1ea-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="fe1ea-132">У вас есть toodelete hello конечная точка, связанная toohello набору балансировки нагрузки из hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-132">You have toodelete hello endpoint associated toohello load balancer set from hello virtual machine.</span></span> <span data-ttu-id="fe1ea-133">После удаления конечной точки hello hello виртуальной машины не принадлежит набор больше toohello с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-133">Once hello endpoint is removed, hello virtual machine doesn't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="fe1ea-134">Используя пример hello выше, можно удалить hello конечной точки, созданной для виртуальной машины «web1» из балансировки нагрузки набор балансировки» нагрузки» с помощью команды hello `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="fe1ea-134">Using hello example above, you can remove hello endpoint created for virtual machine "web1" from load balancer "lbset" using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="fe1ea-135">Вы можете просматривать параметры toomanage конечных точек с помощью команды hello`azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="fe1ea-135">You can explore more options toomanage endpoints using hello command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe1ea-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fe1ea-136">Next steps</span></span>

[<span data-ttu-id="fe1ea-137">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="fe1ea-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="fe1ea-138">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="fe1ea-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="fe1ea-139">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="fe1ea-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
