---
title: "Поиск следующего прыжка с помощью возможности определения следующего прыжка в Наблюдателе за сетями Azure (Azure CLI 2.0) | Документация Майкрософт"
description: "В этой статье описано, как определить тип следующего прыжка и IP-адрес, используя возможность определения следующего прыжка в Azure CLI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d1ee6870ba0188ff2c473e4cca12a5bdc1f97d3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="9dd52-103">Определите тип следующего прыжка, используя возможность определения следующего прыжка в Наблюдателе за сетями Azure в Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="9dd52-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9dd52-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="9dd52-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="9dd52-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dd52-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="9dd52-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="9dd52-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="9dd52-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9dd52-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="9dd52-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="9dd52-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="9dd52-109">Определение следующего прыжка — это возможность Наблюдателя за сетями, позволяющая определить тип следующего прыжка и IP-адрес на основе указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9dd52-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="9dd52-110">Эта возможность используется, чтобы определить путь передачи исходящего трафика виртуальной машины (шлюз, Интернет или виртуальные сети) к месту назначения.</span><span class="sxs-lookup"><span data-stu-id="9dd52-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="9dd52-111">В этой статье мы используем наш новейший интерфейс командной строки для модели развертывания ресурсов и управления ими, а именно Azure CLI 2.0. Этот интерфейс доступен для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="9dd52-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="9dd52-112">Для выполнения действий, описанных в этой статье, требуется [установить интерфейс командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="9dd52-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9dd52-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9dd52-113">Before you begin</span></span>

<span data-ttu-id="9dd52-114">В этом сценарии для определения типа следующего прыжка и IP-адреса используется Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9dd52-114">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="9dd52-115">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create a Network Watcher](network-watcher-create.md) (Создание Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="9dd52-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="9dd52-116">Предполагается также, что у вас есть группа ресурсов с допустимой виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="9dd52-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="9dd52-117">Сценарий</span><span class="sxs-lookup"><span data-stu-id="9dd52-117">Scenario</span></span>

<span data-ttu-id="9dd52-118">В сценарии, описанном в этой статье, используется определение следующего прыжка — возможность Наблюдателя за сетями, которая позволяет определить тип следующего перехода и IP-адрес для ресурса.</span><span class="sxs-lookup"><span data-stu-id="9dd52-118">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="9dd52-119">Дополнительные сведения об определении следующего прыжка см. в [этой статье](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9dd52-119">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="9dd52-120">Получение следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="9dd52-120">Get Next Hop</span></span>

<span data-ttu-id="9dd52-121">Чтобы получить следующий прыжок, вызовите командлет `az network watcher show-next-hop`.</span><span class="sxs-lookup"><span data-stu-id="9dd52-121">To get the next hop we call the `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="9dd52-122">Мы передаем в командлет группу ресурсов Наблюдателя за сетями, Наблюдатель за сетями, идентификатор виртуальной машины, IP-адрес источника и места назначения.</span><span class="sxs-lookup"><span data-stu-id="9dd52-122">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="9dd52-123">В этом примере в качестве IP-адреса места назначения используется IP-адрес виртуальной машины в другой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9dd52-123">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="9dd52-124">Между двумя виртуальными сетями находится шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9dd52-124">There is a virtual network gateway between the two virtual networks.</span></span>

<span data-ttu-id="9dd52-125">Установите и настройте последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) (если вы еще этого не сделали), а затем войдите с использованием учетной записи Azure, выполнив команду [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="9dd52-125">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="9dd52-126">Затем выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="9dd52-126">Then run the following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="9dd52-127">Если в виртуальной машине есть несколько сетевых карт и на любой из них включена IP-пересылка, нужно указать параметр сетевой карты (-i nic-id).</span><span class="sxs-lookup"><span data-stu-id="9dd52-127">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="9dd52-128">В противном случае этот параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="9dd52-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="9dd52-129">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="9dd52-129">Review results</span></span>

<span data-ttu-id="9dd52-130">По завершении выводятся результаты.</span><span class="sxs-lookup"><span data-stu-id="9dd52-130">When complete, the results are provided.</span></span> <span data-ttu-id="9dd52-131">Возвращается IP-адрес следующего прыжка и тип ресурса.</span><span class="sxs-lookup"><span data-stu-id="9dd52-131">The next hop IP address is returned as well as the type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="9dd52-132">Ниже перечислены доступные значения NextHopType.</span><span class="sxs-lookup"><span data-stu-id="9dd52-132">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="9dd52-133">**Типы следующего прыжка**</span><span class="sxs-lookup"><span data-stu-id="9dd52-133">**Next Hop Type**</span></span>

* <span data-ttu-id="9dd52-134">Интернет</span><span class="sxs-lookup"><span data-stu-id="9dd52-134">Internet</span></span>
* <span data-ttu-id="9dd52-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="9dd52-135">VirtualAppliance</span></span>
* <span data-ttu-id="9dd52-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="9dd52-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="9dd52-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="9dd52-137">VnetLocal</span></span>
* <span data-ttu-id="9dd52-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="9dd52-138">HyperNetGateway</span></span>
* <span data-ttu-id="9dd52-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="9dd52-139">VnetPeering</span></span>
* <span data-ttu-id="9dd52-140">None</span><span class="sxs-lookup"><span data-stu-id="9dd52-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dd52-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9dd52-141">Next steps</span></span>

<span data-ttu-id="9dd52-142">Узнайте, как просмотреть параметры группы безопасности сети программным образом, в статье [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Выполнение аудита групп безопасности сети с помощью Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="9dd52-142">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
