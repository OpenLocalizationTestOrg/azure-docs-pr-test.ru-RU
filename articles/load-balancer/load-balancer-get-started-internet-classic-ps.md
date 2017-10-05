---
title: "Создание доступной в Интернете внутренней подсистемы балансировки нагрузки с помощью Azure PowerShell | Документация Майкрософт"
description: "Сведения о создании балансировщика нагрузки для Интернета в классическом режиме с помощью PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 1a41f3ba199fb692c111ea6a40ddb09605f91da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="120ce-103">Приступая к работе по созданию балансировщика нагрузки (классический режим) для Интернета в PowerShell</span><span class="sxs-lookup"><span data-stu-id="120ce-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="120ce-104">классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="120ce-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="120ce-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="120ce-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="120ce-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="120ce-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="120ce-107">облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="120ce-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="120ce-108">Прежде чем приступить к работе с ресурсами Azure, обратите внимание на то, что в настоящее время в Azure существует две модели развертывания: классическая модель развертывания и модель развертывания с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="120ce-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="120ce-109">Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="120ce-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="120ce-110">Для просмотра документации о средствах развертывания выбирайте соответствующие вкладки в верхней части данной статьи.</span><span class="sxs-lookup"><span data-stu-id="120ce-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="120ce-111">В этой статье рассматривается классическая модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="120ce-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="120ce-112">Вы также можете [узнать, как создать балансировщик нагрузки для Интернета с помощью диспетчера ресурсов Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="120ce-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="120ce-113">Настройка балансировки нагрузки с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="120ce-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="120ce-114">Чтобы настроить балансировщик нагрузки с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="120ce-114">To set up a load balancer using powershell, follow the steps below:</span></span>

1. <span data-ttu-id="120ce-115">Если вы ранее не использовали Azure PowerShell, следуйте инструкциям в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview) , чтобы выполнить вход в Azure и выбрать подписку.</span><span class="sxs-lookup"><span data-stu-id="120ce-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="120ce-116">Создав виртуальную машину, можно добавить к ней подсистему балансировки нагрузки в пределах той же облачной службы, используя для этого командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="120ce-116">After creating a virtual machine, you can use PowerShell cmdlets to add a load balancer to a virtual machine within the same cloud service.</span></span>

<span data-ttu-id="120ce-117">В следующем примере набор балансировщика нагрузки именем "webfarm" добавляется в облачную службу "mytestcloud" (или myctestcloud.cloudapp.net) путем добавления конечных точек для балансировщика нагрузки в виртуальные машины "web1" и "web2".</span><span class="sxs-lookup"><span data-stu-id="120ce-117">In the following example you will add a load balancer set called "webfarm" to cloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding the endpoints for the load balancer to virtual machines named "web1" and "web2".</span></span> <span data-ttu-id="120ce-118">Балансировщик нагрузки принимает сетевой трафик через порт 80 и распределяет его между виртуальными машинами, определенными локальной конечной точкой (в данном случае порт 80), по протоколу TCP.</span><span class="sxs-lookup"><span data-stu-id="120ce-118">The load balancer receives network traffic on port 80 and load balances between the virtual machines defined by the local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="120ce-119">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="120ce-119">Step 1</span></span>

<span data-ttu-id="120ce-120">Создайте конечную точку с балансировкой нагрузки для первой виртуальной машины "web1".</span><span class="sxs-lookup"><span data-stu-id="120ce-120">Create a load balanced endpoint for the first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="120ce-121">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="120ce-121">Step 2</span></span>

<span data-ttu-id="120ce-122">Создайте другую конечную точку для второй виртуальной машины "web2" с использованием того же имени набора балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="120ce-122">Create another endpoint for the second VM  "web2" using the same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="120ce-123">Удаление виртуальной машины из балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="120ce-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="120ce-124">Для удаления конечной точки виртуальной машины из балансировщика нагрузки можно использовать Remove-AzureEndpoint.</span><span class="sxs-lookup"><span data-stu-id="120ce-124">You can use Remove-AzureEndpoint to remove a virtual machine endpoint from the load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="120ce-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="120ce-125">Next steps</span></span>

<span data-ttu-id="120ce-126">Вы также можете [приступить к созданию внутреннего балансировщика нагрузки](load-balancer-get-started-ilb-classic-ps.md) и настроить [режим распределения](load-balancer-distribution-mode.md) для определенного поведения балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="120ce-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="120ce-127">Если вашему приложению необходимо поддерживать подключения для серверов за балансировщиком нагрузки, можно получить дополнительные сведения о [параметрах времени ожидания простоя TCP для балансировщика нагрузки](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="120ce-127">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="120ce-128">Вы узнаете о поведении неактивного подключения при использовании балансировщика нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="120ce-128">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
