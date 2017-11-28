---
title: "Подсистема балансировки нагрузки aaaCreate с выходом в Интернет - классический портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate с выходом подсистемы балансировки нагрузки Интернета в классическом развертывании модели с помощью hello классический портал Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a><span data-ttu-id="55f00-103">Приступая к созданию подсистемы балансировки нагрузки (классические) в hello классический портал Azure с выходом в Интернет</span><span class="sxs-lookup"><span data-stu-id="55f00-103">Get started creating an Internet facing load balancer (classic) in hello Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="55f00-104">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="55f00-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="55f00-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="55f00-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="55f00-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="55f00-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="55f00-107">облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="55f00-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="55f00-108">Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчера ресурсов Azure и классическом.</span><span class="sxs-lookup"><span data-stu-id="55f00-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="55f00-109">Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="55f00-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="55f00-110">Для просмотра документации hello для различных средств, щелкнув вкладки hello hello верхней части этой статьи.</span><span class="sxs-lookup"><span data-stu-id="55f00-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="55f00-111">В этой статье рассматриваются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="55f00-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="55f00-112">Вы также можете [Узнайте, как с помощью диспетчера ресурсов Azure подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="55f00-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="55f00-113">Настройка подсистемы балансировки нагрузки, доступной в Интернете, для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="55f00-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="55f00-114">В порядке tooload нагрузку сетевого трафика из hello Интернета на виртуальных машинах hello облачной службы необходимо создать набор балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="55f00-114">In order tooload balance network traffic from hello Internet across hello virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="55f00-115">В этой процедуре предполагается, что вы уже создали hello виртуальные машины и что они являются все внутри hello же облачной службе.</span><span class="sxs-lookup"><span data-stu-id="55f00-115">This procedure assumes that you have already created hello virtual machines and that they are all within hello same cloud service.</span></span>

<span data-ttu-id="55f00-116">**tooconfigure набор балансировки нагрузки для виртуальных машин**</span><span class="sxs-lookup"><span data-stu-id="55f00-116">**tooconfigure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="55f00-117">В hello классический портал Azure, щелкните **виртуальные машины**и щелкните имя виртуальной машины в наборе балансировки нагрузки hello hello.</span><span class="sxs-lookup"><span data-stu-id="55f00-117">In hello Azure classic portal, click **Virtual Machines**, and then click hello name of a virtual machine in hello load-balanced set.</span></span>
2. <span data-ttu-id="55f00-118">Щелкните **Конечные точки**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="55f00-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="55f00-119">На hello **добавить конечную точку tooa виртуальную машину** нажмите кнопку со стрелкой вправо hello.</span><span class="sxs-lookup"><span data-stu-id="55f00-119">On hello **Add an endpoint tooa virtual machine** page, click hello right arrow.</span></span>
4. <span data-ttu-id="55f00-120">На hello **укажите hello подробные сведения о конечной точке hello** страницы:</span><span class="sxs-lookup"><span data-stu-id="55f00-120">On hello **Specify hello details of hello endpoint** page:</span></span>

   * <span data-ttu-id="55f00-121">В **имя**, введите имя для конечной точки hello, или выберите имя hello hello списка предопределенных конечных точек для общих протоколов.</span><span class="sxs-lookup"><span data-stu-id="55f00-121">In **Name**, type a name for hello endpoint or select hello name from hello list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="55f00-122">В **протокола**, выберите протокол hello, предусмотренного hello тип конечной точки, TCP или UDP, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="55f00-122">In **Protocol**, select hello protocol required by hello type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="55f00-123">В **общий порт и частный порт**, введите hello номера портов, которые вы хотите hello toouse виртуальной машине при необходимости.</span><span class="sxs-lookup"><span data-stu-id="55f00-123">In **Public Port and Private Port**, type hello port numbers that you want hello virtual machine toouse, as needed.</span></span> <span data-ttu-id="55f00-124">Можно использовать частный порт hello и правила брандмауэра на hello tooredirect весь трафик виртуальных машин в виде, наиболее подходящий для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="55f00-124">You can use hello private port and firewall rules on hello virtual machine tooredirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="55f00-125">то же, что hello открытый порт может hello Hello частный порт.</span><span class="sxs-lookup"><span data-stu-id="55f00-125">hello private port can be hello same as hello public port.</span></span> <span data-ttu-id="55f00-126">Например для конечной точки для (HTTP) веб-трафика, можно назначить порт 80 tooboth hello открытый и частный порт.</span><span class="sxs-lookup"><span data-stu-id="55f00-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 tooboth hello public and private port.</span></span>

5. <span data-ttu-id="55f00-127">Выберите **создать набор балансировки нагрузки**и нажмите кнопку со стрелкой вправо hello.</span><span class="sxs-lookup"><span data-stu-id="55f00-127">Select **Create a load-balanced set**, and then click hello right arrow.</span></span>
6. <span data-ttu-id="55f00-128">На hello **настроить набор балансировки нагрузки hello** введите имя для набора балансировки нагрузки hello и назначить значения hello для поведения зонда подсистемы балансировки нагрузки Azure hello.</span><span class="sxs-lookup"><span data-stu-id="55f00-128">On hello **Configure hello load-balanced set** page, type a name for hello load-balanced set, and then assign hello values for probe behavior of hello Azure Load Balancer.</span></span> <span data-ttu-id="55f00-129">Hello подсистемы балансировки нагрузки использует зонды toodetermine Если hello виртуальных машин в набор балансировки нагрузки hello доступных tooreceive входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="55f00-129">hello Load Balancer uses probes toodetermine if hello virtual machines in hello load-balanced set are available tooreceive incoming traffic.</span></span>
7. <span data-ttu-id="55f00-130">Выберите конечную балансировкой нагрузки hello флажок toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="55f00-130">Click hello check mark toocreate hello load-balanced endpoint.</span></span> <span data-ttu-id="55f00-131">Вы увидите **Да** в hello **имя набора с балансировкой нагрузки** столбец hello **конечные точки** страница hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="55f00-131">You will see **Yes** in hello **Load-balanced set name** column of hello **Endpoints** page for hello virtual machine.</span></span>
8. <span data-ttu-id="55f00-132">На портале hello щелкните **виртуальные машины**, щелкните имя дополнительной виртуальной машине в набор балансировки нагрузки hello hello, **конечные точки**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="55f00-132">In hello portal, click **Virtual Machines**, click hello name of an additional virtual machine in hello load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="55f00-133">На hello **добавьте виртуальной машине tooa конечной точки** щелкните **добавить набор существующих балансировкой нагрузки конечной точки tooan**, выберите имя набора балансировки нагрузки hello hello и нажмите кнопку со стрелкой вправо hello.</span><span class="sxs-lookup"><span data-stu-id="55f00-133">On hello **Add an endpoint tooa virtual machine** page, click **Add endpoint tooan existing load-balanced set**, select hello name of hello load-balanced set, and then click hello right arrow.</span></span>
10. <span data-ttu-id="55f00-134">На hello **укажите hello подробные сведения о конечной точке hello** введите имя для конечной точки hello и нажмите кнопку флажок hello.</span><span class="sxs-lookup"><span data-stu-id="55f00-134">On hello **Specify hello details of hello endpoint** page, type a name for hello endpoint, and then click hello check mark.</span></span>

<span data-ttu-id="55f00-135">Для hello дополнительных виртуальных машин в набор балансировки нагрузки hello повторите шаги 8-10.</span><span class="sxs-lookup"><span data-stu-id="55f00-135">For hello additional virtual machines in hello load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55f00-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55f00-136">Next steps</span></span>

[<span data-ttu-id="55f00-137">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="55f00-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="55f00-138">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="55f00-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="55f00-139">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="55f00-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
