---
title: "aaaAzure поддержки диспетчера ресурсов для подсистемы балансировки нагрузки | Документы Microsoft"
description: "Использование PowerShell для работы с подсистемой балансировки нагрузки в Azure Resource Manager. Использование шаблонов для подсистемы балансировки нагрузки"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="36c83-104">Использование поддержки Azure Resource Manager с Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="36c83-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="36c83-105">Диспетчер ресурсов Azure — платформа управления предпочтительный hello для служб в Azure.</span><span class="sxs-lookup"><span data-stu-id="36c83-105">Azure Resource Manager is hello preferred management framework for services in Azure.</span></span> <span data-ttu-id="36c83-106">Теперь Azure Load Balancer можно управлять с помощью интерфейсов API и инструментов на основе Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="36c83-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="36c83-107">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="36c83-107">Concepts</span></span>

<span data-ttu-id="36c83-108">С помощью диспетчера ресурсов подсистемы балансировки нагрузки Azure содержит следующие дочерние ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="36c83-108">With Resource Manager, Azure Load Balancer contains hello following child resources:</span></span>

* <span data-ttu-id="36c83-109">Конфигурация внешних IP-адресов: балансировщик нагрузки может включать в себя один или несколько внешних IP-адресов, которые также называются виртуальными IP-адресами.</span><span class="sxs-lookup"><span data-stu-id="36c83-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="36c83-110">Эти IP-адреса используются в качестве входящего трафика hello.</span><span class="sxs-lookup"><span data-stu-id="36c83-110">These IP addresses serve as ingress for hello traffic.</span></span>
* <span data-ttu-id="36c83-111">Пул адресов серверной части — это IP-адресов, связанных с виртуальной машиной hello сети карта (NIC) распределяются toowhich нагрузки.</span><span class="sxs-lookup"><span data-stu-id="36c83-111">Back-end address pool – these are IP addresses associated with hello virtual machine Network Interface Card (NIC) toowhich load will be distributed.</span></span>
* <span data-ttu-id="36c83-112">Балансировка нагрузки правила — правило свойство сопоставляется с IP-адресом данного внешнего интерфейса и порта набор tooa сочетания IP-адресов серверной части и комбинация порт.</span><span class="sxs-lookup"><span data-stu-id="36c83-112">Load balancing rules – a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="36c83-113">Отдельный балансировщик нагрузки может применять несколько правил балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="36c83-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="36c83-114">Каждое правило представляет собой сочетание интерфейсных IP-адреса и порта и внутренних IP-адреса и порта, связанных с виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="36c83-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="36c83-115">Датчики — зонды включить вы tookeep отслеживания работоспособности hello экземпляров виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="36c83-115">Probes – probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="36c83-116">Если происходит сбой проверки работоспособности, hello экземпляр виртуальной Машины будет выполняться автоматически из ротации.</span><span class="sxs-lookup"><span data-stu-id="36c83-116">If a health probe fails, hello VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="36c83-117">Правила NAT для входящего трафика — определение правил NAT hello входящий трафик с IP-адреса внешнего интерфейса hello и обратно распределенных toohello конечный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="36c83-117">Inbound NAT rules – NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="36c83-118">Шаблоны быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="36c83-118">Quickstart templates</span></span>

<span data-ttu-id="36c83-119">Диспетчер ресурсов Azure можно tooprovision приложений с помощью декларативного шаблона.</span><span class="sxs-lookup"><span data-stu-id="36c83-119">Azure Resource Manager allows you tooprovision your applications using a declarative template.</span></span> <span data-ttu-id="36c83-120">В одном шаблоне можно развернуть несколько служб и их зависимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="36c83-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="36c83-121">Использовать hello же toorepeatedly шаблона развертывания приложения на каждом этапе жизненного цикла приложения hello.</span><span class="sxs-lookup"><span data-stu-id="36c83-121">You use hello same template toorepeatedly deploy your application during every stage of hello application lifecycle.</span></span>

<span data-ttu-id="36c83-122">Шаблоны могут содержать определения виртуальных машин, виртуальных сетей, групп доступности, сетевых интерфейсов (сетевых карт), учетных записей хранения, балансировщиков нагрузки, групп безопасности сети и общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="36c83-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="36c83-123">С помощью шаблонов можно создать все необходимое для сложного приложения.</span><span class="sxs-lookup"><span data-stu-id="36c83-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="36c83-124">Hello файл шаблона может проверяться в системе управления содержимым для системы управления версиями и совместной работы.</span><span class="sxs-lookup"><span data-stu-id="36c83-124">hello template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="36c83-125">Дополнительные сведения о шаблонах</span><span class="sxs-lookup"><span data-stu-id="36c83-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="36c83-126">Дополнительные сведения о сетевых ресурсах</span><span class="sxs-lookup"><span data-stu-id="36c83-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="36c83-127">Шаблоны быстрого запуска, использующие Azure Load Balancer, можно найти в [репозитории GitHub](https://github.com/Azure/azure-quickstart-templates) , где размещен набор шаблонов, созданный сообществом.</span><span class="sxs-lookup"><span data-stu-id="36c83-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="36c83-128">Примеры шаблонов:</span><span class="sxs-lookup"><span data-stu-id="36c83-128">Examples of templates:</span></span>

* [<span data-ttu-id="36c83-129">2 ВМ в подсистеме балансировки нагрузки и правила балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="36c83-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="36c83-130">2 ВМ в виртуальной сети с внутренней подсистемой балансировки нагрузки и правилами балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="36c83-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="36c83-131">2 ВМ в подсистему балансировки нагрузки и настроить правила преобразования сетевых адресов на hello балансировки Нагрузки</span><span class="sxs-lookup"><span data-stu-id="36c83-131">2 VMs in a Load Balancer and configure NAT rules on hello LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="36c83-132">Настройка балансировки нагрузки Azure с помощью PowerShell или интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="36c83-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="36c83-133">Приступая к работе с командлетами, программами командной строки и интерфейсами REST API на основе Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36c83-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="36c83-134">[Командлеты Azure к сети](https://msdn.microsoft.com/library/azure/mt163510.aspx) может быть toocreate используется подсистемой балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="36c83-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used toocreate a Load Balancer.</span></span>
* [<span data-ttu-id="36c83-135">Как toocreate подсистемы балансировки нагрузки с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="36c83-135">How toocreate a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="36c83-136">С помощью hello Azure CLI с помощью управления ресурсами Azure</span><span class="sxs-lookup"><span data-stu-id="36c83-136">Using hello Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="36c83-137">Интерфейсы API REST подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="36c83-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="36c83-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36c83-138">Next steps</span></span>

<span data-ttu-id="36c83-139">[Создайте доступную из Интернета подсистему балансировки нагрузки](load-balancer-get-started-internet-arm-ps.md) и настройте тип [режима распределения](load-balancer-distribution-mode.md) для определенного поведения сетевого трафика балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="36c83-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="36c83-140">Узнайте, как toomanage [простоя параметры времени ожидания TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="36c83-140">Learn how toomanage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="36c83-141">Это важно в тех случаях, когда приложению tookeep подключений проверки активности для серверов в подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="36c83-141">This is important when your application needs tookeep connections alive for servers behind a load balancer.</span></span>
