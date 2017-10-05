---
title: "Создание доступной в Интернете внутренней подсистемы балансировки нагрузки с помощью Azure CLI | Документация Майкрософт"
description: "Узнайте, как создать балансировщик нагрузки для Интернета в классической модели развертывания с помощью интерфейса командной строки Azure."
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
ms.openlocfilehash: da3a908f17ff5c6d3923549a884ecc0a13cb8e9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-cli"></a><span data-ttu-id="5908e-103">Приступая к созданию балансировщика нагрузки (классический режим) для Интернета в Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5908e-103">Get started creating an Internet facing load balancer (classic) in the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5908e-104">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="5908e-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="5908e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5908e-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="5908e-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="5908e-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="5908e-107">облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="5908e-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="5908e-108">Прежде чем приступить к работе с ресурсами Azure, обратите внимание на то, что в настоящее время в Azure существует две модели развертывания: классическая модель развертывания и модель развертывания с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5908e-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="5908e-109">Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="5908e-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="5908e-110">Для просмотра документации о средствах развертывания выбирайте соответствующие вкладки в верхней части данной статьи.</span><span class="sxs-lookup"><span data-stu-id="5908e-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="5908e-111">В этой статье рассматривается классическая модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="5908e-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="5908e-112">Вы также можете [узнать, как создать балансировщик нагрузки для Интернета с помощью диспетчера ресурсов Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5908e-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="5908e-113">Пошаговая процедура создания балансировщика нагрузки для Интернета с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="5908e-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="5908e-114">Это руководство описывает создание балансировщика нагрузки для Интернета на основе приведенного выше сценария.</span><span class="sxs-lookup"><span data-stu-id="5908e-114">This guide shows how to create an Internet load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="5908e-115">Если вы еще не пользовались Azure CLI, ознакомьтесь со статьей [Установка и настройка CLI Azure](../cli-install-nodejs.md) и следуйте инструкциям вплоть до выбора учетной записи Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="5908e-115">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="5908e-116">Выполните команду **azure config mode** , чтобы переключиться в классический режим, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5908e-116">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="5908e-117">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5908e-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="5908e-118">Создание набора балансировщика нагрузки и конечной точки</span><span class="sxs-lookup"><span data-stu-id="5908e-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="5908e-119">Сценарий предполагает, что были созданы виртуальные машины "web1" и "web2".</span><span class="sxs-lookup"><span data-stu-id="5908e-119">The scenario assumes the virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="5908e-120">В этом руководстве будет создан набор балансировщика нагрузки с использованием общего порта 80 и локального порта 80.</span><span class="sxs-lookup"><span data-stu-id="5908e-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="5908e-121">Для пробы также задается порт 80, а набору балансировщика нагрузки присваивается имя lbset.</span><span class="sxs-lookup"><span data-stu-id="5908e-121">A probe port is also configured on port 80 and named the load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="5908e-122">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="5908e-122">Step 1</span></span>

<span data-ttu-id="5908e-123">Создайте первую конечную точку и набор балансировщика нагрузки, используя `azure network vm endpoint create` для виртуальной машины web1.</span><span class="sxs-lookup"><span data-stu-id="5908e-123">Create the first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="5908e-124">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="5908e-124">Step 2</span></span>

<span data-ttu-id="5908e-125">Добавьте в набор балансировщика нагрузки вторую виртуальную машину "web2".</span><span class="sxs-lookup"><span data-stu-id="5908e-125">Add a second virtual machine "web2" to the load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="5908e-126">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="5908e-126">Step 3</span></span>

<span data-ttu-id="5908e-127">Проверьте конфигурацию балансировщика нагрузки с помощью `azure vm show` .</span><span class="sxs-lookup"><span data-stu-id="5908e-127">Verify the load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="5908e-128">Выходные данные должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5908e-128">The output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="5908e-129">Создание конечной точки удаленного рабочего стола для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="5908e-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="5908e-130">Вы можете создать конечную точку удаленного рабочего стола для пересылки трафика с общего порта на локальный порт для конкретной виртуальной машины с помощью `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="5908e-130">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="5908e-131">Удаление виртуальной машины из балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="5908e-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="5908e-132">Вам необходимо удалить конечную точку, сопоставленную с набором балансировщика нагрузки, из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5908e-132">You have to delete the endpoint associated to the load balancer set from the virtual machine.</span></span> <span data-ttu-id="5908e-133">После удаления конечной точки виртуальная машина больше не входит в набор балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5908e-133">Once the endpoint is removed, the virtual machine doesn't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="5908e-134">Используя приведенный выше пример, можно удалить конечную точку, созданную для виртуальной машины "web1", из "lbset" балансировщика нагрузки с помощью команды `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="5908e-134">Using the example above, you can remove the endpoint created for virtual machine "web1" from load balancer "lbset" using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="5908e-135">Вы можете отобразить дополнительные параметры для управления конечными точками с помощью команды `azure vm endpoint --help`.</span><span class="sxs-lookup"><span data-stu-id="5908e-135">You can explore more options to manage endpoints using the command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="5908e-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5908e-136">Next steps</span></span>

[<span data-ttu-id="5908e-137">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="5908e-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="5908e-138">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="5908e-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="5908e-139">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="5908e-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
