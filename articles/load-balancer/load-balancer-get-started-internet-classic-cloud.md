---
title: "Создание доступной в Интернете внутренней подсистемы балансировки нагрузки для облачных служб Azure | Документация Майкрософт"
description: "Сведения о создании балансировщика нагрузки для Интернета по классической модели развертывания для облачных служб"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 1ceaafebcaebecb04314c7da62c69b2e9b5ba39a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="51f10-103">Приступая к работе по созданию балансировщика нагрузки для Интернета для облачных служб</span><span class="sxs-lookup"><span data-stu-id="51f10-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="51f10-104">классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="51f10-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="51f10-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51f10-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="51f10-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="51f10-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="51f10-107">облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="51f10-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="51f10-108">Прежде чем приступить к работе с ресурсами Azure, обратите внимание на то, что в настоящее время в Azure существует две модели развертывания: классическая модель развертывания и модель развертывания с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="51f10-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="51f10-109">Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="51f10-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="51f10-110">Для просмотра документации о средствах развертывания выбирайте соответствующие вкладки в верхней части данной статьи.</span><span class="sxs-lookup"><span data-stu-id="51f10-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="51f10-111">В этой статье рассматривается классическая модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="51f10-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="51f10-112">Вы также можете [узнать, как создать балансировщик нагрузки для Интернета с помощью диспетчера ресурсов Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="51f10-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="51f10-113">Облачные службы автоматически настраиваются с помощью подсистемы балансировки нагрузки. Их также можно настроить, используя модель службы.</span><span class="sxs-lookup"><span data-stu-id="51f10-113">Cloud services are automatically configured with a load balancer and can be customized via the service model.</span></span>

## <a name="create-a-load-balancer-using-the-service-definition-file"></a><span data-ttu-id="51f10-114">Создайте балансировщик нагрузки при помощи CSDEF-файла</span><span class="sxs-lookup"><span data-stu-id="51f10-114">Create a load balancer using the service definition file</span></span>

<span data-ttu-id="51f10-115">Вы можете обновить облачную службу с помощью пакета Azure SDK для .NET 2.5.</span><span class="sxs-lookup"><span data-stu-id="51f10-115">You can leverage the Azure SDK for .NET 2.5 to update your cloud service.</span></span> <span data-ttu-id="51f10-116">Настройки конечных точек для облачных служб создаются в CSDEF-файле [определения службы](https://msdn.microsoft.com/library/azure/gg557553.aspx).</span><span class="sxs-lookup"><span data-stu-id="51f10-116">Endpoint settings for cloud services are made in the [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="51f10-117">В следующем примере показано, как настроить файл servicedefinition.csdef для облачного развертывания.</span><span class="sxs-lookup"><span data-stu-id="51f10-117">The following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="51f10-118">Во фрагменте CSDEF-файла, созданного путем облачного развертывания, можно увидеть внешнюю конечную точку, настроенную для использования портов HTTP через порты 10000, 10001 и 10002.</span><span class="sxs-lookup"><span data-stu-id="51f10-118">Checking the snippet for the .csdef file generated by a cloud deployment, you can see the external endpoint configured to use ports HTTP on port 10000, 10001, and 10002.</span></span>

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="51f10-119">Проверка состояния работоспособности подсистемы балансировки нагрузки для облачных служб</span><span class="sxs-lookup"><span data-stu-id="51f10-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="51f10-120">Пример зонда работоспособности:</span><span class="sxs-lookup"><span data-stu-id="51f10-120">The following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="51f10-121">Балансировщик нагрузки объединяет сведения о конечной точке и сведения о зонде для создания URL-адреса в виде `http://{DIP of VM}:80/Probe.aspx`, который можно использовать для запроса на проверку работоспособности службы.</span><span class="sxs-lookup"><span data-stu-id="51f10-121">The load balancer combines the information of the endpoint and the information of the probe to create a URL in the form of `http://{DIP of VM}:80/Probe.aspx` that can be used to query the health of the service.</span></span>

<span data-ttu-id="51f10-122">Служба обнаруживает периодические зонды с одного и того же IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="51f10-122">The service detects periodic probes from the same IP address.</span></span> <span data-ttu-id="51f10-123">Это запрос зонда работоспособности, поступающий от узла, на котором запущена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="51f10-123">This is the health probe request coming from the host of the node where the virtual machine is running.</span></span> <span data-ttu-id="51f10-124">Служба должна отправить ответ с кодом состояния HTTP 200, что подтверждает для подсистемы балансировки нагрузки, что служба работоспособна.</span><span class="sxs-lookup"><span data-stu-id="51f10-124">The service has to respond with a HTTP 200 status code for the load balancer to assume that the service is healthy.</span></span> <span data-ttu-id="51f10-125">Любой другой код состояния HTTP (например, 503) непосредственно выводит виртуальную машину из ротации.</span><span class="sxs-lookup"><span data-stu-id="51f10-125">Any other HTTP status code (for example 503) directly takes the virtual machine out of rotation.</span></span>

<span data-ttu-id="51f10-126">С помощью определения зонда можно контролировать частоту отправки зондов.</span><span class="sxs-lookup"><span data-stu-id="51f10-126">The probe definition also controls the frequency of the probe.</span></span> <span data-ttu-id="51f10-127">В описанном выше случае подсистема балансировки нагрузки зондирует конечную точку каждые 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="51f10-127">In our case above, the load balancer is probing the endpoint every 5 secs.</span></span> <span data-ttu-id="51f10-128">Если в течение 10 секунд не приходит положительный ответ (два интервала зонда), предполагается, что зонд завершился сбоем, и виртуальная машина перестает использоваться.</span><span class="sxs-lookup"><span data-stu-id="51f10-128">If no positive answer is received for 10 secs (two probe intervals), the probe is assumed down, and the virtual machine is taken out of rotation.</span></span> <span data-ttu-id="51f10-129">Аналогично, если получен положительный ответ для службы, которая не используется, сразу же выполняется ее автоматический запуск.</span><span class="sxs-lookup"><span data-stu-id="51f10-129">Similarly, if the service is out of rotation and a positive answer is received, the service is put back to rotation right away.</span></span> <span data-ttu-id="51f10-130">Если состояние службы постоянно меняется (с рабочего на нерабочее и наоборот), подсистема балансировки нагрузки может отложить повторный запуск службы до получения определенного количества ответов, подтверждающих ее работоспособность.</span><span class="sxs-lookup"><span data-stu-id="51f10-130">If the service is fluctuating between healthy and unhealthy, the load balancer can decide to delay the re-introduction of the service back to rotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="51f10-131">Чтобы получить дополнительную информацию о [зонде работоспособности](https://msdn.microsoft.com/library/azure/jj151530.aspx), см. схему определения службы.</span><span class="sxs-lookup"><span data-stu-id="51f10-131">Check the service definition schema for the [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51f10-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="51f10-132">Next steps</span></span>

[<span data-ttu-id="51f10-133">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="51f10-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="51f10-134">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="51f10-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="51f10-135">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="51f10-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

