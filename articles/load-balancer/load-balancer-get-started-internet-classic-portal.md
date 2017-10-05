---
title: "Создание доступной в Интернете внутренней подсистемы балансировки нагрузки с помощью классического портала Azure | Документация Майкрософт"
description: "Узнайте, как создать балансировщика нагрузки для Интернета в классической модели развертывания с помощью классического портала Azure."
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
ms.openlocfilehash: a022154f5eca6de2d2dbfc1b9aa30d2ea0a7d650
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-classic-portal"></a><span data-ttu-id="0d9d8-103">Приступая к созданию балансировщика нагрузки (классический режим) для Интернета на классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="0d9d8-103">Get started creating an Internet facing load balancer (classic) in the Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d9d8-104">классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="0d9d8-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="0d9d8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d9d8-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="0d9d8-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="0d9d8-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="0d9d8-107">облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="0d9d8-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="0d9d8-108">Прежде чем приступить к работе с ресурсами Azure, обратите внимание на то, что в настоящее время в Azure существует две модели развертывания: классическая модель развертывания и модель развертывания с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="0d9d8-109">Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="0d9d8-110">Для просмотра документации о средствах развертывания выбирайте соответствующие вкладки в верхней части данной статьи.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="0d9d8-111">В этой статье рассматривается классическая модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="0d9d8-112">Вы также можете [узнать, как создать балансировщик нагрузки для Интернета с помощью диспетчера ресурсов Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0d9d8-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="0d9d8-113">Настройка подсистемы балансировки нагрузки, доступной в Интернете, для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0d9d8-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="0d9d8-114">Чтобы распределить нагрузку сетевого трафика из Интернета между виртуальными машинами облачной службы, нужно создать набор балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-114">In order to load balance network traffic from the Internet across the virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="0d9d8-115">В этой процедуре предполагается, что вы уже создали виртуальные машины и что все они находятся в одной облачной службе.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-115">This procedure assumes that you have already created the virtual machines and that they are all within the same cloud service.</span></span>

<span data-ttu-id="0d9d8-116">**Настройка набора балансировки нагрузки для виртуальных машин**</span><span class="sxs-lookup"><span data-stu-id="0d9d8-116">**To configure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="0d9d8-117">На классическом портале Azure щелкните **Виртуальные машины**, а затем выберите имя виртуальной машины в наборе балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-117">In the Azure classic portal, click **Virtual Machines**, and then click the name of a virtual machine in the load-balanced set.</span></span>
2. <span data-ttu-id="0d9d8-118">Щелкните **Конечные точки**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="0d9d8-119">На странице **Добавление конечной точки к виртуальной машине** нажмите стрелку вправо.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-119">On the **Add an endpoint to a virtual machine** page, click the right arrow.</span></span>
4. <span data-ttu-id="0d9d8-120">На странице **Ввод сведений о конечной точке** укажите следующую информацию.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-120">On the **Specify the details of the endpoint** page:</span></span>

   * <span data-ttu-id="0d9d8-121">В поле **Имя**введите имя конечной точки или выберите имя в списке предварительно определенных конечных точек для распространенных протоколов.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-121">In **Name**, type a name for the endpoint or select the name from the list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="0d9d8-122">В поле **Протокол**выберите при необходимости протокол, который требуется для этого типа конечной точки (TCP или UDP).</span><span class="sxs-lookup"><span data-stu-id="0d9d8-122">In **Protocol**, select the protocol required by the type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="0d9d8-123">В полях **Общий порт и Частный порт**введите при необходимости номера портов, которые требуется использовать для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-123">In **Public Port and Private Port**, type the port numbers that you want the virtual machine to use, as needed.</span></span> <span data-ttu-id="0d9d8-124">На виртуальной машине можно использовать частный порт и правила брандмауэра, чтобы перенаправить трафик способом, который подходит для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-124">You can use the private port and firewall rules on the virtual machine to redirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="0d9d8-125">Частный порт может быть таким же, как общий порт.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-125">The private port can be the same as the public port.</span></span> <span data-ttu-id="0d9d8-126">Например, для конечной точки для веб-трафика (HTTP) для общего и частного порта можно назначить порт 80.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 to both the public and private port.</span></span>

5. <span data-ttu-id="0d9d8-127">Выберите **Создать набор балансировки нагрузки**и нажмите стрелку вправо.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-127">Select **Create a load-balanced set**, and then click the right arrow.</span></span>
6. <span data-ttu-id="0d9d8-128">На странице **Настроить набор балансировки нагрузки** введите имя для набора балансировки нагрузки, а затем присвойте значения для поведения зондов подсистемы балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-128">On the **Configure the load-balanced set** page, type a name for the load-balanced set, and then assign the values for probe behavior of the Azure Load Balancer.</span></span> <span data-ttu-id="0d9d8-129">Подсистема балансировки нагрузки использует пробы для определения, доступны ли виртуальные машины в наборе балансировки нагрузки для приема входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-129">The Load Balancer uses probes to determine if the virtual machines in the load-balanced set are available to receive incoming traffic.</span></span>
7. <span data-ttu-id="0d9d8-130">Чтобы создать конечную точку балансировки нагрузки, поставьте галочку.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-130">Click the check mark to create the load-balanced endpoint.</span></span> <span data-ttu-id="0d9d8-131">Вы увидите **Да** в столбце **Имя набора балансировки нагрузки** на странице **Конечные точки** виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-131">You will see **Yes** in the **Load-balanced set name** column of the **Endpoints** page for the virtual machine.</span></span>
8. <span data-ttu-id="0d9d8-132">На портале управления щелкните **Виртуальные машины**, выберите имя дополнительной виртуальной машины в наборе балансировки нагрузки, а затем щелкните **Конечные точки** и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-132">In the portal, click **Virtual Machines**, click the name of an additional virtual machine in the load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="0d9d8-133">На странице **Добавить конечную точку на виртуальную машину** нажмите **Добавить конечную точку в существующий набор балансировки нагрузки**, выберите имя набора балансировки нагрузки и щелкните стрелку вправо.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-133">On the **Add an endpoint to a virtual machine** page, click **Add endpoint to an existing load-balanced set**, select the name of the load-balanced set, and then click the right arrow.</span></span>
10. <span data-ttu-id="0d9d8-134">На странице **Ввод сведений о конечной точке** введите имя конечной точки и щелкните флажок.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-134">On the **Specify the details of the endpoint** page, type a name for the endpoint, and then click the check mark.</span></span>

<span data-ttu-id="0d9d8-135">Для дополнительных виртуальных машин в наборе балансировки нагрузки повторите шаги 8–10.</span><span class="sxs-lookup"><span data-stu-id="0d9d8-135">For the additional virtual machines in the load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d9d8-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0d9d8-136">Next steps</span></span>

[<span data-ttu-id="0d9d8-137">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="0d9d8-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="0d9d8-138">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="0d9d8-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="0d9d8-139">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="0d9d8-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
