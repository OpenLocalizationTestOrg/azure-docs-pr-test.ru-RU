---
title: "Поддержка Azure Resource Manager для балансировщика нагрузки | Документация Майкрософт"
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
ms.openlocfilehash: d06c924f384a2684b5a91c202039c581796c1091
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="14198-104">Использование поддержки Azure Resource Manager с Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="14198-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="14198-105">Azure Resource Manager представляет собой предпочтительную платформу управления для служб в Azure.</span><span class="sxs-lookup"><span data-stu-id="14198-105">Azure Resource Manager is the preferred management framework for services in Azure.</span></span> <span data-ttu-id="14198-106">Теперь Azure Load Balancer можно управлять с помощью интерфейсов API и инструментов на основе Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="14198-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="14198-107">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="14198-107">Concepts</span></span>

<span data-ttu-id="14198-108">Azure Load Balancer с Resource Manager содержит следующие дочерние ресурсы.</span><span class="sxs-lookup"><span data-stu-id="14198-108">With Resource Manager, Azure Load Balancer contains the following child resources:</span></span>

* <span data-ttu-id="14198-109">Конфигурация внешних IP-адресов: балансировщик нагрузки может включать в себя один или несколько внешних IP-адресов, которые также называются виртуальными IP-адресами.</span><span class="sxs-lookup"><span data-stu-id="14198-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="14198-110">Такие IP-адреса обеспечивают поступление трафика.</span><span class="sxs-lookup"><span data-stu-id="14198-110">These IP addresses serve as ingress for the traffic.</span></span>
* <span data-ttu-id="14198-111">Пул внутренних адресов: это IP-адреса, связанные с сетевыми картами виртуальных машин, между которыми распределяется нагрузка.</span><span class="sxs-lookup"><span data-stu-id="14198-111">Back-end address pool – these are IP addresses associated with the virtual machine Network Interface Card (NIC) to which load will be distributed.</span></span>
* <span data-ttu-id="14198-112">Правила балансировки нагрузки: свойство правила сопоставляет указанное сочетание внешнего IP-адреса и порта с набором серверных IP-адресов и портов.</span><span class="sxs-lookup"><span data-stu-id="14198-112">Load balancing rules – a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="14198-113">Отдельный балансировщик нагрузки может применять несколько правил балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="14198-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="14198-114">Каждое правило представляет собой сочетание интерфейсных IP-адреса и порта и внутренних IP-адреса и порта, связанных с виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="14198-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="14198-115">Пробы: пробы позволяют отслеживать работоспособность экземпляров виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="14198-115">Probes – probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="14198-116">В случае сбоя пробы работоспособности экземпляр виртуальной машины автоматически перестает использоваться.</span><span class="sxs-lookup"><span data-stu-id="14198-116">If a health probe fails, the VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="14198-117">Правила NAT для входящего трафика: правила NAT, определяющие входящий трафик, который проходит через внешний IP-адрес и передается серверному IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="14198-117">Inbound NAT rules – NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="14198-118">Шаблоны быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="14198-118">Quickstart templates</span></span>

<span data-ttu-id="14198-119">Диспетчер ресурсов Azure позволяет подготавливать приложения с помощью декларативного шаблона.</span><span class="sxs-lookup"><span data-stu-id="14198-119">Azure Resource Manager allows you to provision your applications using a declarative template.</span></span> <span data-ttu-id="14198-120">В одном шаблоне можно развернуть несколько служб и их зависимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="14198-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="14198-121">Один шаблон используется для развертывания приложения на каждом этапе его жизненного цикла.</span><span class="sxs-lookup"><span data-stu-id="14198-121">You use the same template to repeatedly deploy your application during every stage of the application lifecycle.</span></span>

<span data-ttu-id="14198-122">Шаблоны могут содержать определения виртуальных машин, виртуальных сетей, групп доступности, сетевых интерфейсов (сетевых карт), учетных записей хранения, балансировщиков нагрузки, групп безопасности сети и общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="14198-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="14198-123">С помощью шаблонов можно создать все необходимое для сложного приложения.</span><span class="sxs-lookup"><span data-stu-id="14198-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="14198-124">Файл шаблона можно вернуть в систему управления содержимым, чтобы обеспечить управление версиями и возможность совместной работы.</span><span class="sxs-lookup"><span data-stu-id="14198-124">The template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="14198-125">Дополнительные сведения о шаблонах</span><span class="sxs-lookup"><span data-stu-id="14198-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="14198-126">Дополнительные сведения о сетевых ресурсах</span><span class="sxs-lookup"><span data-stu-id="14198-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="14198-127">Шаблоны быстрого запуска, использующие Azure Load Balancer, можно найти в [репозитории GitHub](https://github.com/Azure/azure-quickstart-templates) , где размещен набор шаблонов, созданный сообществом.</span><span class="sxs-lookup"><span data-stu-id="14198-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="14198-128">Примеры шаблонов:</span><span class="sxs-lookup"><span data-stu-id="14198-128">Examples of templates:</span></span>

* [<span data-ttu-id="14198-129">2 ВМ в подсистеме балансировки нагрузки и правила балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="14198-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="14198-130">2 ВМ в виртуальной сети с внутренней подсистемой балансировки нагрузки и правилами балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="14198-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="14198-131">2 ВМ в подсистеме балансировки нагрузки и правила преобразования сетевых адресов для балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="14198-131">2 VMs in a Load Balancer and configure NAT rules on the LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="14198-132">Настройка балансировки нагрузки Azure с помощью PowerShell или интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="14198-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="14198-133">Приступая к работе с командлетами, программами командной строки и интерфейсами REST API на основе Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="14198-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="14198-134">[Сетевые командлеты Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) можно использовать для создания подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="14198-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used to create a Load Balancer.</span></span>
* [<span data-ttu-id="14198-135">Создание подсистемы балансировки нагрузки с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="14198-135">How to create a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="14198-136">Использование Azure CLI с диспетчером ресурсов Azure (ARM)</span><span class="sxs-lookup"><span data-stu-id="14198-136">Using the Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="14198-137">Интерфейсы API REST подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="14198-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="14198-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="14198-138">Next steps</span></span>

<span data-ttu-id="14198-139">[Создайте доступную из Интернета подсистему балансировки нагрузки](load-balancer-get-started-internet-arm-ps.md) и настройте тип [режима распределения](load-balancer-distribution-mode.md) для определенного поведения сетевого трафика балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="14198-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="14198-140">Узнайте, как управлять [временем ожидания простоя TCP для балансировщика нагрузки](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="14198-140">Learn how to manage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="14198-141">Это важно в тех случаях, когда приложению требуется проверять активность подключений к серверам, управляемым балансировщиком нагрузки.</span><span class="sxs-lookup"><span data-stu-id="14198-141">This is important when your application needs to keep connections alive for servers behind a load balancer.</span></span>
