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
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a><span data-ttu-id="7730c-103">Приступая к созданию внутренней подсистемы балансировки нагрузки (классической) с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7730c-103">Get started creating an internal load balancer (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7730c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7730c-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="7730c-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="7730c-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="7730c-106">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="7730c-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="7730c-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7730c-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7730c-108">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="7730c-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="7730c-109">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7730c-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="7730c-110">Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7730c-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="7730c-111">toocreate внутренний балансировщик нагрузки для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="7730c-111">toocreate an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="7730c-112">toocreate внутренний балансировщик нагрузки задать и hello серверов, которые будут отправлять их tooit трафика, необходимо выполнить следующие hello:</span><span class="sxs-lookup"><span data-stu-id="7730c-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you must do hello following:</span></span>

1. <span data-ttu-id="7730c-113">Создайте экземпляр внутренней балансировки нагрузки, конечную точку hello входящего трафика toobe Балансировка нагрузки для серверов hello набора балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7730c-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="7730c-114">Добавьте конечные точки, соответствующие toohello виртуальных машин, которые будут принимать входящий трафик hello.</span><span class="sxs-lookup"><span data-stu-id="7730c-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="7730c-115">Настройка серверов hello, которые будут отправлять что hello трафика toobe с балансировкой нагрузки toosend их трафика toohello виртуальных IP-адресов (VIP) адрес экземпляра hello внутренней балансировки.</span><span class="sxs-lookup"><span data-stu-id="7730c-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="7730c-116">Пошаговая процедура создания внутреннего балансировщика нагрузки с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="7730c-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="7730c-117">В этом руководстве показано, как toocreate внутренний балансировщик нагрузки на основе hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="7730c-117">This guide shows how toocreate an internal load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="7730c-118">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="7730c-118">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="7730c-119">Запустите hello **azure конфигурации режима** режим tooclassic команд tooswitch, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="7730c-119">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="7730c-120">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="7730c-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="7730c-121">Создание набора балансировщика нагрузки и конечной точки</span><span class="sxs-lookup"><span data-stu-id="7730c-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="7730c-122">Hello сценарий предполагает hello виртуальные машины «DB1» и «DB2» в облачной службе, называется «mytestcloud».</span><span class="sxs-lookup"><span data-stu-id="7730c-122">hello scenario assumes hello virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="7730c-123">Обе виртуальные машины используют виртуальную сеть с именем "testvnet" с подсетью "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="7730c-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="7730c-124">В этом руководстве будет создан набор внутренних балансировщиков нагрузки с использованием порта 1433 в качестве частного порта и порта 1433 в качестве локального порта.</span><span class="sxs-lookup"><span data-stu-id="7730c-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="7730c-125">Это общие сценарии, где имеется SQL виртуальных машин на hello серверной части, используя внутренней нагрузки серверов балансировки tooguarantee hello базы данных не будет предоставляться напрямую, используя общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="7730c-125">This is a common scenario where you have SQL virtual machines on hello back end using an internal load balancer tooguarantee hello database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="7730c-126">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="7730c-126">Step 1</span></span>

<span data-ttu-id="7730c-127">Создайте набор внутренних балансировщиков нагрузки с помощью `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="7730c-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="7730c-128">Дополнительные сведения см. в `azure service internal-load-balancer --help`.</span><span class="sxs-lookup"><span data-stu-id="7730c-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="7730c-129">Вы можете проверить hello свойства внутреннего балансировщика нагрузки с помощью команды hello `azure service internal-load-balancer list` *имя облачной службы*.</span><span class="sxs-lookup"><span data-stu-id="7730c-129">You can check hello internal load balancer properties using hello command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="7730c-130">Здесь пример hello выходных данных выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7730c-130">Here follows an example of hello output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="7730c-131">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="7730c-131">Step 2</span></span>

<span data-ttu-id="7730c-132">Настройки hello внутренней подсистемы балансировки нагрузки задается при добавлении hello первую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="7730c-132">You configure hello internal load balancer set when you add hello first endpoint.</span></span> <span data-ttu-id="7730c-133">Будет связывать hello конечной точки, виртуальной машины и проверки порт toohello внутренний набор балансировщиков нагрузки на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="7730c-133">You will associate hello endpoint, virtual machine and probe port toohello internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="7730c-134">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="7730c-134">Step 3</span></span>

<span data-ttu-id="7730c-135">Проверьте hello нагрузки балансировки конфигурации с помощью `azure vm show` *имя виртуальной машины*</span><span class="sxs-lookup"><span data-stu-id="7730c-135">Verify hello load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="7730c-136">Hello выходные данные будут:</span><span class="sxs-lookup"><span data-stu-id="7730c-136">hello output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="7730c-137">Создание конечной точки удаленного рабочего стола для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7730c-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="7730c-138">Вы можете создать удаленного рабочего стола конечной точки tooforward сетевого трафика на локальный порт tooa открытый порт для конкретной виртуальной машины с помощью `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="7730c-138">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="7730c-139">Удаление виртуальной машины из балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="7730c-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="7730c-140">Можно удалить виртуальную машину из внутренний набор балансировщиков нагрузки путем удаления связанных hello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="7730c-140">You can remove a virtual machine from an internal load balancer set by deleting hello associated endpoint.</span></span> <span data-ttu-id="7730c-141">После удаления конечной точки hello hello виртуальной машины не принадлежит набор больше toohello с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7730c-141">Once hello endpoint is removed, hello virtual machine won't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="7730c-142">С помощью приведенном выше примере hello, можно удалить hello конечной точки, созданной для виртуальной машины «DB1» из внутренней подсистемы балансировки нагрузки «ilbset» с помощью команды hello `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="7730c-142">Using hello example above, you can remove hello endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="7730c-143">Дополнительные сведения см. в `azure vm endpoint --help`.</span><span class="sxs-lookup"><span data-stu-id="7730c-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7730c-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7730c-144">Next steps</span></span>

[<span data-ttu-id="7730c-145">Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу</span><span class="sxs-lookup"><span data-stu-id="7730c-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="7730c-146">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="7730c-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
