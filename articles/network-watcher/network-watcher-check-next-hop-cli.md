---
title: "Следующий прыжок aaaFind с Azure сети наблюдателя следующего прыжка — Azure CLI 2.0 | Документы Microsoft"
description: "В этой статье описывается, как можно найти какие hello тип следующего прыжка — и адрес ip с помощью следующего прыжка с помощью Azure CLI."
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
ms.openlocfilehash: 77c2bde51274bd5c64e7a2467f95139af620ca30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="48da6-103">Узнать, какой тип следующего прыжка hello является использование возможностей следующего прыжка hello в Наблюдатель сети Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="48da6-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="48da6-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="48da6-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="48da6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48da6-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="48da6-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="48da6-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="48da6-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="48da6-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="48da6-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="48da6-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="48da6-109">Следующий прыжок является компонентом Наблюдатель сети, который предоставляет возможность hello получить тип следующего прыжка hello и IP-адрес, на основе указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="48da6-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="48da6-110">Эта функция полезна при определении Если пакетов, отправляемых виртуальная машина проходит через шлюз, Интернет или назначения tooits tooget виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="48da6-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="48da6-111">В этой статье используется нашей следующего поколения CLI для модели развертывания управления ресурса hello Azure CLI 2.0, которая доступна для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="48da6-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="48da6-112">tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="48da6-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="48da6-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="48da6-113">Before you begin</span></span>

<span data-ttu-id="48da6-114">В этом сценарии используется hello тип следующего прыжка Azure CLI toofind hello и IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="48da6-114">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="48da6-115">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="48da6-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="48da6-116">сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.</span><span class="sxs-lookup"><span data-stu-id="48da6-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="48da6-117">Сценарий</span><span class="sxs-lookup"><span data-stu-id="48da6-117">Scenario</span></span>

<span data-ttu-id="48da6-118">Hello сценарии, описанные в данной статье используется следующего прыжка, функция Наблюдатель сети, извлекают тип следующего прыжка hello и IP-адрес для ресурса.</span><span class="sxs-lookup"><span data-stu-id="48da6-118">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="48da6-119">Посетите toolearn Дополнительные сведения о следующего прыжка [следующего прыжка Обзор](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48da6-119">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="48da6-120">Получение следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="48da6-120">Get Next Hop</span></span>

<span data-ttu-id="48da6-121">Следующий прыжок tooget hello мы называем hello `az network watcher show-next-hop` командлета.</span><span class="sxs-lookup"><span data-stu-id="48da6-121">tooget hello next hop we call hello `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="48da6-122">Мы передаем группы ресурсов Наблюдатель сети hello командлет hello, hello NetworkWatcher, виртуальной машины идентификатор, исходный IP-адрес и IP-адрес назначения.</span><span class="sxs-lookup"><span data-stu-id="48da6-122">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="48da6-123">В этом примере hello конечный IP-адрес — tooa виртуальной Машины в другой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="48da6-123">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="48da6-124">Нет шлюза виртуальной сети между двумя виртуальными сетями hello.</span><span class="sxs-lookup"><span data-stu-id="48da6-124">There is a virtual network gateway between hello two virtual networks.</span></span>

<span data-ttu-id="48da6-125">Если еще не еще, установить и настроить hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="48da6-125">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="48da6-126">Затем выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="48da6-126">Then run hello following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="48da6-127">Если hello виртуальной Машины имеет несколько сетевых адаптеров и IP-пересылки включен на всех сетевых адаптеров hello, hello параметров сетевого Адаптера (-я nic-id) должно быть указано.</span><span class="sxs-lookup"><span data-stu-id="48da6-127">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="48da6-128">В противном случае этот параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="48da6-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="48da6-129">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="48da6-129">Review results</span></span>

<span data-ttu-id="48da6-130">По завершении приведены результаты hello.</span><span class="sxs-lookup"><span data-stu-id="48da6-130">When complete, hello results are provided.</span></span> <span data-ttu-id="48da6-131">а также hello тип ресурса, который является возвращается IP-адрес следующего прыжка Hello.</span><span class="sxs-lookup"><span data-stu-id="48da6-131">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="48da6-132">Hello ниже перечислены в настоящее время доступных значений NextHopType hello.</span><span class="sxs-lookup"><span data-stu-id="48da6-132">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="48da6-133">**Типы следующего прыжка**</span><span class="sxs-lookup"><span data-stu-id="48da6-133">**Next Hop Type**</span></span>

* <span data-ttu-id="48da6-134">Интернет</span><span class="sxs-lookup"><span data-stu-id="48da6-134">Internet</span></span>
* <span data-ttu-id="48da6-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="48da6-135">VirtualAppliance</span></span>
* <span data-ttu-id="48da6-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="48da6-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="48da6-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="48da6-137">VnetLocal</span></span>
* <span data-ttu-id="48da6-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="48da6-138">HyperNetGateway</span></span>
* <span data-ttu-id="48da6-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="48da6-139">VnetPeering</span></span>
* <span data-ttu-id="48da6-140">None</span><span class="sxs-lookup"><span data-stu-id="48da6-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="48da6-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48da6-141">Next steps</span></span>

<span data-ttu-id="48da6-142">Узнайте, как tooreview параметров группы безопасности сети программным способом, посетив [NSG аудита и Наблюдатель сети](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="48da6-142">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
