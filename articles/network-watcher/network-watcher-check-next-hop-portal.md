---
title: "Следующий прыжок aaaFind с Azure сети наблюдателя следующего прыжка - портал Azure | Документы Microsoft"
description: "В этой статье описывается, как можно найти какие hello тип следующего прыжка — и IP-адрес, с помощью следующего прыжка hello портал Azure"
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
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="8fa0a-103">Узнать, какой тип следующего прыжка hello является использование возможностей следующего прыжка hello в Наблюдатель сети Azure с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="8fa0a-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8fa0a-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="8fa0a-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="8fa0a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8fa0a-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="8fa0a-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="8fa0a-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="8fa0a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8fa0a-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="8fa0a-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="8fa0a-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="8fa0a-109">Следующий прыжок является компонентом Наблюдатель сети, который предоставляет возможность hello получить тип следующего прыжка hello и IP-адрес, на основе указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="8fa0a-110">Эта функция полезна при определении Если пакетов, отправляемых виртуальная машина проходит через шлюз, Интернет или назначения tooits tooget виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8fa0a-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="8fa0a-111">Before you begin</span></span>

<span data-ttu-id="8fa0a-112">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-112">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="8fa0a-113">сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-113">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="8fa0a-114">Сценарий</span><span class="sxs-lookup"><span data-stu-id="8fa0a-114">Scenario</span></span>

<span data-ttu-id="8fa0a-115">Hello сценарии, описанные в данной статье используется следующего прыжка toofind тип следующего прыжка hello и IP-адрес для ресурса.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-115">hello scenario covered in this article uses Next hop toofind out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="8fa0a-116">Посетите toolearn Дополнительные сведения о следующего прыжка [следующего прыжка Обзор](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8fa0a-116">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="8fa0a-117">Вам предстоит:</span><span class="sxs-lookup"><span data-stu-id="8fa0a-117">In this scenario, you will:</span></span>

* <span data-ttu-id="8fa0a-118">Получение следующего прыжка hello из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-118">Retrieve hello next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="8fa0a-119">Получение следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="8fa0a-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="8fa0a-120">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="8fa0a-120">Step 1</span></span>

<span data-ttu-id="8fa0a-121">Перейдите tooyour Наблюдатель сети ресурс в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-121">Navigate tooyour Network Watcher resource in hello Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="8fa0a-122">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="8fa0a-122">Step 2</span></span>

<span data-ttu-id="8fa0a-123">Нажмите кнопку **следующего прыжка** в области навигации hello hello выберите виртуальную машину и сетевого интерфейса, введите hello исходного и конечного IP и нажмите кнопку hello **следующего прыжка** кнопки.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-123">Click **Next hop** in hello navigation pane, select hello virtual machine and network interface, fill out hello source and destination IP, and click hello **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="8fa0a-124">Следующий прыжок требуется что toorun распределения ресурсов виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-124">Next hop requires that hello VM resource is allocated toorun.</span></span>

![Обзор получения следующего прыжка][1]

### <a name="step-3"></a><span data-ttu-id="8fa0a-126">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-126">Step 3</span></span>

<span data-ttu-id="8fa0a-127">После завершения задачи hello приведены результаты hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-127">Once hello task is complete, hello results are provided.</span></span> <span data-ttu-id="8fa0a-128">Здравствуйте, IP-адрес и тип следующего прыжка hello устройство, отображается.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-128">hello IP address and type of device hello next hop is, is displayed.</span></span> <span data-ttu-id="8fa0a-129">Hello следующей таблице показаны доступные возвращенные значения hello в портал hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-129">hello following table shows hello available returned values in hello portal.</span></span>

<span data-ttu-id="8fa0a-130">**Типы следующего прыжка**</span><span class="sxs-lookup"><span data-stu-id="8fa0a-130">**Next Hop Type**</span></span>

* <span data-ttu-id="8fa0a-131">Интернет</span><span class="sxs-lookup"><span data-stu-id="8fa0a-131">Internet</span></span>
* <span data-ttu-id="8fa0a-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="8fa0a-132">VirtualAppliance</span></span>
* <span data-ttu-id="8fa0a-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="8fa0a-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="8fa0a-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="8fa0a-134">VnetLocal</span></span>
* <span data-ttu-id="8fa0a-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="8fa0a-135">HyperNetGateway</span></span>
* <span data-ttu-id="8fa0a-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="8fa0a-136">VnetPeering</span></span>
* <span data-ttu-id="8fa0a-137">None</span><span class="sxs-lookup"><span data-stu-id="8fa0a-137">None</span></span>

<span data-ttu-id="8fa0a-138">Если настраиваемый маршрут был используется tooroute этот трафик hello определяемых пользователем маршрутов (UDR) также отображаются с результатами hello.</span><span class="sxs-lookup"><span data-stu-id="8fa0a-138">If a custom route was used tooroute this traffic, hello User-defined route (UDR) is shown as well with hello results.</span></span>

![Получение результатов следующего прыжка][2]

## <a name="next-steps"></a><span data-ttu-id="8fa0a-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8fa0a-140">Next steps</span></span>

<span data-ttu-id="8fa0a-141">Узнайте, как tooreview параметров группы безопасности сети программным способом, посетив [NSG аудита и Наблюдатель сети](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8fa0a-141">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














