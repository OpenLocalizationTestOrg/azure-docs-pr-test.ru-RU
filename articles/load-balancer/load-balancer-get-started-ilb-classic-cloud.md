---
title: "Создание внутренней подсистемы балансировки нагрузки для облачных служб Azure | Документация Майкрософт"
description: "Узнайте, как создать внутренний балансировщик нагрузки в классической модели развертывания с помощью PowerShell."
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
ms.openlocfilehash: 8dbc951416d577fa7f534c2eab1605c6bee61fce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="8aced-103">Начало работы по созданию внутреннего балансировщика нагрузки (классическая версия) для облачных служб</span><span class="sxs-lookup"><span data-stu-id="8aced-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8aced-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8aced-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="8aced-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8aced-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="8aced-106">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="8aced-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="8aced-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8aced-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8aced-108">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="8aced-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="8aced-109">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8aced-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8aced-110">Узнайте, как [выполнить эти действия с помощью модели Resource Manager](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8aced-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="8aced-111">Настройка внутреннего балансировщика нагрузки для облачных служб</span><span class="sxs-lookup"><span data-stu-id="8aced-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="8aced-112">Внутренний балансировщик нагрузки поддерживается как для виртуальных машин, так и для облачных служб.</span><span class="sxs-lookup"><span data-stu-id="8aced-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="8aced-113">Доступ к конечной точке внутреннего балансировщика, созданной в облачной службе за пределами региональной виртуальной сети, можно будет получить только из этой облачной службы.</span><span class="sxs-lookup"><span data-stu-id="8aced-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within the cloud service.</span></span>

<span data-ttu-id="8aced-114">Конфигурацию внутреннего балансировщика нагрузки необходимо задавать во время создания первого развертывания в облачной службе, как показано в приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="8aced-114">The internal load balancer configuration has to be set during the creation of the first deployment in the cloud service, as shown in the sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8aced-115">Для выполнения указанных ниже действий необходимо, чтобы виртуальная сеть была создана и готова к облачному развертыванию.</span><span class="sxs-lookup"><span data-stu-id="8aced-115">A prerequisite to run the steps below is to have a virtual network already created for the cloud deployment.</span></span> <span data-ttu-id="8aced-116">Для создания внутренней балансировки нагрузки потребуется имя виртуальной сети и имя подсети.</span><span class="sxs-lookup"><span data-stu-id="8aced-116">You will need the virtual network name and subnet name to create the Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="8aced-117">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="8aced-117">Step 1</span></span>

<span data-ttu-id="8aced-118">Откройте файл конфигурации службы (с расширением CSCFG) для облачного развертывания в Visual Studio и добавьте под последним элементом`</Role>`в конфигурации сети приведенный ниже раздел, чтобы создать внутреннюю балансировку нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8aced-118">Open the service configuration file (.cscfg) for your cloud deployment in Visual Studio and add the following section to create the Internal Load Balancing under the last "`</Role>`" item for the network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of the load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="8aced-119">Добавим значения в файл конфигурации сети, чтобы показать, как он будет выглядеть.</span><span class="sxs-lookup"><span data-stu-id="8aced-119">Let's add the values for the network configuration file to show how it will look.</span></span> <span data-ttu-id="8aced-120">Предположим, вы создали виртуальную сеть с именем test_vnet и подсетью 10.0.0.0/24 с именем test_subnet и статическим IP-адресом 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="8aced-120">In the example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="8aced-121">Подсистема балансировки нагрузки будет называться testLB.</span><span class="sxs-lookup"><span data-stu-id="8aced-121">The load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="8aced-122">Дополнительные сведения о схеме балансировщика нагрузки см. в статье [Добавление подсистемы балансировки нагрузки](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span><span class="sxs-lookup"><span data-stu-id="8aced-122">For more information about the load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="8aced-123">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="8aced-123">Step 2</span></span>

<span data-ttu-id="8aced-124">Добавьте в CSDEF-файл конечные точки для подсистемы внутренней балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8aced-124">Change the service definition (.csdef) file to add endpoints to the Internal Load Balancing.</span></span> <span data-ttu-id="8aced-125">При создании экземпляра роли CSDEF-файл добавляет его в подсистему внутренней балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8aced-125">The moment a role instance is created, the service definition file will add the role instances to the Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="8aced-126">Добавим значения из приведенного выше примера в CSDEF-файл.</span><span class="sxs-lookup"><span data-stu-id="8aced-126">Following the same values from the example above, let's add the values to the service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="8aced-127">Балансировка сетевого трафика будет осуществляться с использованием балансировщика нагрузки testLB. При этом порт 80 будет использоваться как для получения входящих запросов, так и для их отправки в экземпляры рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="8aced-127">The network traffic will be load balanced using the testLB load balancer using port 80 for incoming requests, sending to worker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8aced-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8aced-128">Next steps</span></span>

[<span data-ttu-id="8aced-129">Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу</span><span class="sxs-lookup"><span data-stu-id="8aced-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="8aced-130">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8aced-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

