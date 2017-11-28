---
title: "Поиск следующего прыжка с помощью возможности определения следующего прыжка Наблюдателя за сетями Azure (портал Azure) | Документация Майкрософт"
description: "В этой статье описано, как определить тип следующего прыжка и IP-адрес, используя возможность определения следующего прыжка на портале Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5434b7972346821985c459fc4620805adb88676b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-the-portal"></a><span data-ttu-id="59080-103">Определите тип следующего прыжка, используя возможность определения следующего прыжка Наблюдателя за сетями на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="59080-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="59080-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="59080-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="59080-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="59080-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="59080-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="59080-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="59080-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="59080-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="59080-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="59080-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="59080-109">Определение следующего прыжка — это возможность Наблюдателя за сетями, позволяющая определить тип следующего прыжка и IP-адрес на основе указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="59080-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="59080-110">Эта возможность используется, чтобы определить путь передачи исходящего трафика виртуальной машины (шлюз, Интернет или виртуальные сети) к месту назначения.</span><span class="sxs-lookup"><span data-stu-id="59080-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="59080-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="59080-111">Before you begin</span></span>

<span data-ttu-id="59080-112">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create an Azure Network Watcher instance](network-watcher-create.md) (Наблюдатель за сетями: создание экземпляра службы).</span><span class="sxs-lookup"><span data-stu-id="59080-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="59080-113">Предполагается также, что у вас есть группа ресурсов с допустимой виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="59080-113">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="59080-114">Сценарий</span><span class="sxs-lookup"><span data-stu-id="59080-114">Scenario</span></span>

<span data-ttu-id="59080-115">В сценарии, описанном в этой статье, используется возможность определения следующего прыжка, которая позволяет определить тип следующего перехода и IP-адрес ресурса.</span><span class="sxs-lookup"><span data-stu-id="59080-115">The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="59080-116">Дополнительные сведения об определении следующего прыжка см. в [этой статье](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59080-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="59080-117">Вам предстоит:</span><span class="sxs-lookup"><span data-stu-id="59080-117">In this scenario, you will:</span></span>

* <span data-ttu-id="59080-118">получить следующий прыжок виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="59080-118">Retrieve the next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="59080-119">Получение следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="59080-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="59080-120">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="59080-120">Step 1</span></span>

<span data-ttu-id="59080-121">На портале Azure перейдите к своему ресурсу Наблюдателя за сетями.</span><span class="sxs-lookup"><span data-stu-id="59080-121">Navigate to your Network Watcher resource in the Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="59080-122">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="59080-122">Step 2</span></span>

<span data-ttu-id="59080-123">В области навигации щелкните **Следующий прыжок**, выберите интерфейс виртуальной машины или сетевой интерфейс, введите IP-адрес источника и места назначения, а затем нажмите кнопку **Следующий прыжок**.</span><span class="sxs-lookup"><span data-stu-id="59080-123">Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="59080-124">Для получения следующего прыжка необходимо, чтобы ресурс виртуальной машины был выделен.</span><span class="sxs-lookup"><span data-stu-id="59080-124">Next hop requires that the VM resource is allocated to run.</span></span>

![Обзор получения следующего прыжка][1]

### <a name="step-3"></a><span data-ttu-id="59080-126">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="59080-126">Step 3</span></span>

<span data-ttu-id="59080-127">По завершении задания выводятся результаты.</span><span class="sxs-lookup"><span data-stu-id="59080-127">Once the task is complete, the results are provided.</span></span> <span data-ttu-id="59080-128">Здесь вы можете просмотреть IP-адрес устройства и тип следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="59080-128">The IP address and type of device the next hop is, is displayed.</span></span> <span data-ttu-id="59080-129">Ниже приведен список доступных значений, возвращенных на портал.</span><span class="sxs-lookup"><span data-stu-id="59080-129">The following table shows the available returned values in the portal.</span></span>

<span data-ttu-id="59080-130">**Типы следующего прыжка**</span><span class="sxs-lookup"><span data-stu-id="59080-130">**Next Hop Type**</span></span>

* <span data-ttu-id="59080-131">Интернет</span><span class="sxs-lookup"><span data-stu-id="59080-131">Internet</span></span>
* <span data-ttu-id="59080-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="59080-132">VirtualAppliance</span></span>
* <span data-ttu-id="59080-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="59080-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="59080-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="59080-134">VnetLocal</span></span>
* <span data-ttu-id="59080-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="59080-135">HyperNetGateway</span></span>
* <span data-ttu-id="59080-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="59080-136">VnetPeering</span></span>
* <span data-ttu-id="59080-137">None</span><span class="sxs-lookup"><span data-stu-id="59080-137">None</span></span>

<span data-ttu-id="59080-138">Если для маршрутизации трафика использовался определяемый пользователем маршрут, в результатах также отображаются сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="59080-138">If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.</span></span>

![Получение результатов следующего прыжка][2]

## <a name="next-steps"></a><span data-ttu-id="59080-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59080-140">Next steps</span></span>

<span data-ttu-id="59080-141">Узнайте, как просмотреть параметры группы безопасности сети программным образом, в статье [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Выполнение аудита групп безопасности сети с помощью Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="59080-141">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














