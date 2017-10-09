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
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="8c97f-103">Начало работы по созданию внутреннего балансировщика нагрузки (классическая версия) для облачных служб</span><span class="sxs-lookup"><span data-stu-id="8c97f-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c97f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c97f-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="8c97f-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8c97f-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="8c97f-106">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="8c97f-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="8c97f-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8c97f-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8c97f-108">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="8c97f-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="8c97f-109">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8c97f-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="8c97f-110">Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8c97f-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="8c97f-111">Настройка внутреннего балансировщика нагрузки для облачных служб</span><span class="sxs-lookup"><span data-stu-id="8c97f-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="8c97f-112">Внутренний балансировщик нагрузки поддерживается как для виртуальных машин, так и для облачных служб.</span><span class="sxs-lookup"><span data-stu-id="8c97f-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="8c97f-113">Внутренняя нагрузки балансировки конечной точки, созданной в облачной службе, который находится за пределами региональной виртуальной сети будут доступны только в пределах hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="8c97f-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within hello cloud service.</span></span>

<span data-ttu-id="8c97f-114">конфигурация подсистемы балансировки нагрузки внутренней Hello имеет toobe задать во время создания hello hello первого развертывания в облачной службе hello, как показано в следующем примере hello.</span><span class="sxs-lookup"><span data-stu-id="8c97f-114">hello internal load balancer configuration has toobe set during hello creation of hello first deployment in hello cloud service, as shown in hello sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c97f-115">Следующие действия hello готовности toorun — toohave виртуальная сеть уже создан для развертывания облака hello.</span><span class="sxs-lookup"><span data-stu-id="8c97f-115">A prerequisite toorun hello steps below is toohave a virtual network already created for hello cloud deployment.</span></span> <span data-ttu-id="8c97f-116">Вам потребуется hello виртуального сетевого имени и подсети имя toocreate hello внутренней балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8c97f-116">You will need hello virtual network name and subnet name toocreate hello Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c97f-117">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="8c97f-117">Step 1</span></span>

<span data-ttu-id="8c97f-118">Откройте hello файла конфигурации службы (csfg) для развертывания облака в Visual Studio и добавьте следующий раздел toocreate hello внутренней балансировки нагрузки в группе hello последнего hello "`</Role>`" элемента конфигурации сети hello.</span><span class="sxs-lookup"><span data-stu-id="8c97f-118">Open hello service configuration file (.cscfg) for your cloud deployment in Visual Studio and add hello following section toocreate hello Internal Load Balancing under hello last "`</Role>`" item for hello network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="8c97f-119">Давайте добавим hello значения для hello конфигурации сети файла tooshow, как будет выглядеть.</span><span class="sxs-lookup"><span data-stu-id="8c97f-119">Let's add hello values for hello network configuration file tooshow how it will look.</span></span> <span data-ttu-id="8c97f-120">В примере hello предполагается, что вы создали виртуальную сеть, называется «test_vnet» с подсети 10.0.0.0/24 test_subnet и статический IP-адрес 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="8c97f-120">In hello example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="8c97f-121">Подсистема балансировки нагрузки Hello будет называться testLB.</span><span class="sxs-lookup"><span data-stu-id="8c97f-121">hello load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="8c97f-122">Дополнительные сведения о схеме подсистемы балансировки нагрузки hello см. в разделе [балансировки нагрузки добавить](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c97f-122">For more information about hello load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="8c97f-123">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="8c97f-123">Step 2</span></span>

<span data-ttu-id="8c97f-124">Изменение конечных точек hello службы определения службы(.csdef) файл tooadd toohello с внутренней балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8c97f-124">Change hello service definition (.csdef) file tooadd endpoints toohello Internal Load Balancing.</span></span> <span data-ttu-id="8c97f-125">Hello момент создания экземпляра роли, добавляет файл определения службы hello hello роль экземпляров toohello внутренняя Балансировка нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8c97f-125">hello moment a role instance is created, hello service definition file will add hello role instances toohello Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="8c97f-126">Следующие hello же значения в приведенном выше примере hello добавим файл определения службы toohello значения hello.</span><span class="sxs-lookup"><span data-stu-id="8c97f-126">Following hello same values from hello example above, let's add hello values toohello service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="8c97f-127">Hello сетевой трафик будет с помощью подсистемы балансировки нагрузки hello testLB использовать порт 80 для входящих запросов, отправка tooworker экземпляры роли также через порт 80 с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8c97f-127">hello network traffic will be load balanced using hello testLB load balancer using port 80 for incoming requests, sending tooworker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c97f-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8c97f-128">Next steps</span></span>

[<span data-ttu-id="8c97f-129">Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу</span><span class="sxs-lookup"><span data-stu-id="8c97f-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="8c97f-130">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8c97f-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

