---
title: "Подсистема балансировки - нагрузки на aaaCreate из Интернета, Azure PowerShell классический | Документы Microsoft"
description: "Узнайте, как из Интернета toocreate Подсистема балансировки загрузки в классическом режиме, с помощью PowerShell"
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
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="139f0-103">Приступая к работе по созданию балансировщика нагрузки (классический режим) для Интернета в PowerShell</span><span class="sxs-lookup"><span data-stu-id="139f0-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="139f0-104">классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="139f0-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="139f0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="139f0-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="139f0-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="139f0-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="139f0-107">облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="139f0-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="139f0-108">Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчера ресурсов Azure и классическом.</span><span class="sxs-lookup"><span data-stu-id="139f0-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="139f0-109">Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="139f0-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="139f0-110">Для просмотра документации hello для различных средств, щелкнув вкладки hello hello верхней части этой статьи.</span><span class="sxs-lookup"><span data-stu-id="139f0-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="139f0-111">В этой статье рассматриваются hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="139f0-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="139f0-112">Вы также можете [Узнайте, как с помощью диспетчера ресурсов Azure подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="139f0-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="139f0-113">Настройка балансировки нагрузки с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="139f0-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="139f0-114">tooset копирование подсистемы балансировки нагрузки с помощью powershell, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="139f0-114">tooset up a load balancer using powershell, follow hello steps below:</span></span>

1. <span data-ttu-id="139f0-115">Если ранее не пользовались Azure PowerShell, см. раздел [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) и следуйте инструкциям hello все toohello hello способом завершения toosign в Azure и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="139f0-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="139f0-116">После создания виртуальной машины, можно использовать командлеты PowerShell tooadd виртуальной машины tooa подсистемы балансировки нагрузки в пределах hello же облачной службе.</span><span class="sxs-lookup"><span data-stu-id="139f0-116">After creating a virtual machine, you can use PowerShell cmdlets tooadd a load balancer tooa virtual machine within hello same cloud service.</span></span>

<span data-ttu-id="139f0-117">В hello примере будут добавлены набор балансировки нагрузки вызывается toocloud «веб-ферма» «mytestcloud» (или myctestcloud.cloudapp.net), добавление toovirtual подсистемы балансировки нагрузки, hello конечных точек для hello машины службы с именем «web1» и «web2».</span><span class="sxs-lookup"><span data-stu-id="139f0-117">In hello following example you will add a load balancer set called "webfarm" toocloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding hello endpoints for hello load balancer toovirtual machines named "web1" and "web2".</span></span> <span data-ttu-id="139f0-118">Hello балансировки нагрузки получает сетевой трафик через порт 80 и равномерно распределяется между виртуальными машинами hello определяется hello локальную конечную точку (в этом вариантов порт 80) с использованием TCP.</span><span class="sxs-lookup"><span data-stu-id="139f0-118">hello load balancer receives network traffic on port 80 and load balances between hello virtual machines defined by hello local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="139f0-119">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="139f0-119">Step 1</span></span>

<span data-ttu-id="139f0-120">Создание конечной точки балансировки нагрузки для hello первой виртуальной Машины «web1»</span><span class="sxs-lookup"><span data-stu-id="139f0-120">Create a load balanced endpoint for hello first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="139f0-121">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="139f0-121">Step 2</span></span>

<span data-ttu-id="139f0-122">Создайте другой конечной точкой hello второй виртуальной Машины «web2» с помощью hello же нагрузки имя набора балансировки</span><span class="sxs-lookup"><span data-stu-id="139f0-122">Create another endpoint for hello second VM  "web2" using hello same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="139f0-123">Удаление виртуальной машины из балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="139f0-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="139f0-124">Можно использовать Remove-AzureEndpoint tooremove конечной точки виртуальной машины из балансировки нагрузки hello</span><span class="sxs-lookup"><span data-stu-id="139f0-124">You can use Remove-AzureEndpoint tooremove a virtual machine endpoint from hello load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="139f0-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="139f0-125">Next steps</span></span>

<span data-ttu-id="139f0-126">Вы также можете [приступить к созданию внутреннего балансировщика нагрузки](load-balancer-get-started-ilb-classic-ps.md) и настроить [режим распределения](load-balancer-distribution-mode.md) для определенного поведения балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="139f0-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="139f0-127">Если приложению tookeep подключений проверки активности для серверов в подсистему балансировки нагрузки, можно понять больше о [простоя параметры времени ожидания TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="139f0-127">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="139f0-128">Это поможет toolearn о поведении простоя подключения при использовании подсистемы балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="139f0-128">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
