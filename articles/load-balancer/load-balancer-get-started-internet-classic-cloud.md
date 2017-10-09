---
title: "Подсистема балансировки нагрузки aaaCreate из Интернета для облачных служб Azure | Документы Microsoft"
description: "Узнайте, как из Интернета toocreate Подсистема балансировки загрузки в классической модели развертывания для облачных служб"
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
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="814ed-103">Приступая к работе по созданию балансировщика нагрузки для Интернета для облачных служб</span><span class="sxs-lookup"><span data-stu-id="814ed-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="814ed-104">классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="814ed-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="814ed-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="814ed-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="814ed-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="814ed-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="814ed-107">облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="814ed-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="814ed-108">Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчера ресурсов Azure и классическом.</span><span class="sxs-lookup"><span data-stu-id="814ed-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="814ed-109">Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="814ed-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="814ed-110">Для просмотра документации hello для различных средств, щелкнув вкладки hello hello верхней части этой статьи.</span><span class="sxs-lookup"><span data-stu-id="814ed-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="814ed-111">В этой статье рассматриваются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="814ed-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="814ed-112">Вы также можете [Узнайте, как с помощью диспетчера ресурсов Azure подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="814ed-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="814ed-113">Облачные службы автоматически настраиваются с подсистемой балансировки нагрузки и можно настроить через модель службы hello.</span><span class="sxs-lookup"><span data-stu-id="814ed-113">Cloud services are automatically configured with a load balancer and can be customized via hello service model.</span></span>

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a><span data-ttu-id="814ed-114">Создание с помощью файла определения службы hello подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="814ed-114">Create a load balancer using hello service definition file</span></span>

<span data-ttu-id="814ed-115">Вы можете использовать hello Azure SDK для .NET 2,5 tooupdate облачной службы.</span><span class="sxs-lookup"><span data-stu-id="814ed-115">You can leverage hello Azure SDK for .NET 2.5 tooupdate your cloud service.</span></span> <span data-ttu-id="814ed-116">Параметры конечной точки для облачных служб, выполняемых в hello [службы определение](https://msdn.microsoft.com/library/azure/gg557553.aspx) файл csdef.</span><span class="sxs-lookup"><span data-stu-id="814ed-116">Endpoint settings for cloud services are made in hello [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="814ed-117">Hello следующем примере показано, как настроить файл servicedefinition.csdef для развертывания облака:</span><span class="sxs-lookup"><span data-stu-id="814ed-117">hello following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="814ed-118">Проверка фрагмент кода hello для hello файл csdef, созданный при развертывании облака, вы увидите hello внешней конечной точки, настроенной toouse порты HTTP через порт 10000 10001 и 10002.</span><span class="sxs-lookup"><span data-stu-id="814ed-118">Checking hello snippet for hello .csdef file generated by a cloud deployment, you can see hello external endpoint configured toouse ports HTTP on port 10000, 10001, and 10002.</span></span>

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

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="814ed-119">Проверка состояния работоспособности подсистемы балансировки нагрузки для облачных служб</span><span class="sxs-lookup"><span data-stu-id="814ed-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="814ed-120">Hello ниже приведен пример проверки работоспособности:</span><span class="sxs-lookup"><span data-stu-id="814ed-120">hello following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="814ed-121">Hello балансировки нагрузки объединяет сведения hello hello конечной точки и hello toocreate hello проверки URL-адреса в форме hello `http://{DIP of VM}:80/Probe.aspx` , может быть используется tooquery hello работоспособности службы hello.</span><span class="sxs-lookup"><span data-stu-id="814ed-121">hello load balancer combines hello information of hello endpoint and hello information of hello probe toocreate a URL in hello form of `http://{DIP of VM}:80/Probe.aspx` that can be used tooquery hello health of hello service.</span></span>

<span data-ttu-id="814ed-122">Hello служба обнаруживает периодической проверки из hello же IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="814ed-122">hello service detects periodic probes from hello same IP address.</span></span> <span data-ttu-id="814ed-123">Это запрос проверки работоспособности hello, поступающих от узла hello узла hello запущенным hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="814ed-123">This is hello health probe request coming from hello host of hello node where hello virtual machine is running.</span></span> <span data-ttu-id="814ed-124">Служба Hello имеет toorespond с кодом состояния HTTP 200 для tooassume подсистемы балансировки нагрузки hello, что служба hello находится в работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="814ed-124">hello service has toorespond with a HTTP 200 status code for hello load balancer tooassume that hello service is healthy.</span></span> <span data-ttu-id="814ed-125">Все другие состояния HTTP код (например 503) напрямую принимает hello виртуальной машины из ротации.</span><span class="sxs-lookup"><span data-stu-id="814ed-125">Any other HTTP status code (for example 503) directly takes hello virtual machine out of rotation.</span></span>

<span data-ttu-id="814ed-126">Определение проверки Hello также управляет hello частоту выборки hello.</span><span class="sxs-lookup"><span data-stu-id="814ed-126">hello probe definition also controls hello frequency of hello probe.</span></span> <span data-ttu-id="814ed-127">В нашем случае выше hello балансировки нагрузки проверка конечной точки hello каждые 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="814ed-127">In our case above, hello load balancer is probing hello endpoint every 5 secs.</span></span> <span data-ttu-id="814ed-128">Если нет утвердительный ответ, полученный для 10 секунд (двух интервалов выборки), проверки hello предполагается вниз и hello виртуальной машины берется из ротации.</span><span class="sxs-lookup"><span data-stu-id="814ed-128">If no positive answer is received for 10 secs (two probe intervals), hello probe is assumed down, and hello virtual machine is taken out of rotation.</span></span> <span data-ttu-id="814ed-129">Аналогичным образом Если служба hello из ротации и утвердительный ответ, служба hello помещается обратно toorotation прямо сейчас.</span><span class="sxs-lookup"><span data-stu-id="814ed-129">Similarly, if hello service is out of rotation and a positive answer is received, hello service is put back toorotation right away.</span></span> <span data-ttu-id="814ed-130">Если службы hello нагрузка колеблется между Работоспособная и Неработоспособная, подсистемы балансировки нагрузки hello вправе toodelay hello повторное введение задней toorotation hello службы до работоспособны, чтобы число проб.</span><span class="sxs-lookup"><span data-stu-id="814ed-130">If hello service is fluctuating between healthy and unhealthy, hello load balancer can decide toodelay hello re-introduction of hello service back toorotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="814ed-131">Проверьте hello схема определения службы для hello [проверки работоспособности](https://msdn.microsoft.com/library/azure/jj151530.aspx) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="814ed-131">Check hello service definition schema for hello [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="814ed-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="814ed-132">Next steps</span></span>

[<span data-ttu-id="814ed-133">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="814ed-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="814ed-134">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="814ed-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="814ed-135">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="814ed-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

