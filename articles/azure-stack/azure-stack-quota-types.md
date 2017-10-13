---
title: "Типы квот в стек Azure | Документы Microsoft"
description: "Просмотрите типы разные квоты, доступные для службы и ресурсы в Azure стека."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/23/2017
ms.author: erikje
ms.openlocfilehash: 33906514955b76a3d6587b19899a0c76a09018a2
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="quota-types-in-azure-stack"></a><span data-ttu-id="688b3-103">Типы квот в стек Azure</span><span class="sxs-lookup"><span data-stu-id="688b3-103">Quota types in Azure Stack</span></span>

<span data-ttu-id="688b3-104">*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*</span><span class="sxs-lookup"><span data-stu-id="688b3-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="688b3-105">[Квоты](azure-stack-plan-offer-quota-overview.md#plans) определить максимальное количество ресурсов, которые можно подготовить или использовать подписку пользователя.</span><span class="sxs-lookup"><span data-stu-id="688b3-105">[Quotas](azure-stack-plan-offer-quota-overview.md#plans) define the limits of resources that a user subscription can provision or consume.</span></span> <span data-ttu-id="688b3-106">Например квоту может позволить пользователю создавать до пяти виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="688b3-106">For example, a quota might allow a user to create up to five VMs.</span></span> <span data-ttu-id="688b3-107">Каждый ресурс может иметь собственные типы квот.</span><span class="sxs-lookup"><span data-stu-id="688b3-107">Each resource can have its own types of quotas.</span></span>

## <a name="compute-quota-types"></a><span data-ttu-id="688b3-108">Типы квот вычислений</span><span class="sxs-lookup"><span data-stu-id="688b3-108">Compute quota types</span></span>
| <span data-ttu-id="688b3-109">**Тип**</span><span class="sxs-lookup"><span data-stu-id="688b3-109">**Type**</span></span> | <span data-ttu-id="688b3-110">**Значение по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="688b3-110">**Default value**</span></span> | <span data-ttu-id="688b3-111">**Описание**</span><span class="sxs-lookup"><span data-stu-id="688b3-111">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="688b3-112">Максимальное число виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="688b3-112">Max number of virtual machines</span></span> |<span data-ttu-id="688b3-113">50</span><span class="sxs-lookup"><span data-stu-id="688b3-113">50</span></span> | <span data-ttu-id="688b3-114">Максимальное число виртуальных машин, которые можно создать подписки в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-114">The maximum number of virtual machines that a subscription can create in this location.</span></span> |
| <span data-ttu-id="688b3-115">Максимальное число ядер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="688b3-115">Max number of virtual machine cores</span></span> |<span data-ttu-id="688b3-116">100</span><span class="sxs-lookup"><span data-stu-id="688b3-116">100</span></span> | <span data-ttu-id="688b3-117">Максимальное количество ядер, которые можно создать подписки в этом расположении (например, Виртуальной машине A3 имеет четыре ядра).</span><span class="sxs-lookup"><span data-stu-id="688b3-117">The maximum number of cores that a subscription can create in this location (for example, an A3 VM has four cores).</span></span> |
| <span data-ttu-id="688b3-118">Задает максимальное число доступности</span><span class="sxs-lookup"><span data-stu-id="688b3-118">Max number of availability sets</span></span> |<span data-ttu-id="688b3-119">10</span><span class="sxs-lookup"><span data-stu-id="688b3-119">10</span></span> | <span data-ttu-id="688b3-120">Максимальное количество групп доступности, которые могут быть созданы в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-120">The maximum number of availability sets that can be created in this location.</span></span> |
| <span data-ttu-id="688b3-121">Задает максимальное число масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="688b3-121">Max number of virtual machine scale sets</span></span> |<span data-ttu-id="688b3-122">100</span><span class="sxs-lookup"><span data-stu-id="688b3-122">100</span></span> | <span data-ttu-id="688b3-123">Максимальное число наборы масштабирования виртуальных машин, которые могут быть созданы в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-123">The maximum number of virtual machine scale sets that can be created in this location.</span></span> |

> [!NOTE]
> <span data-ttu-id="688b3-124">Вычислений в этой предварительной технической версии не применяются квоты.</span><span class="sxs-lookup"><span data-stu-id="688b3-124">Compute quotas are not enforced in this technical preview.</span></span>
> 
> 

## <a name="storage-quota-types"></a><span data-ttu-id="688b3-125">Типы квота хранилища</span><span class="sxs-lookup"><span data-stu-id="688b3-125">Storage quota types</span></span>
| <span data-ttu-id="688b3-126">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="688b3-126">**Item**</span></span> | <span data-ttu-id="688b3-127">**Значение по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="688b3-127">**Default value**</span></span> | <span data-ttu-id="688b3-128">**Описание**</span><span class="sxs-lookup"><span data-stu-id="688b3-128">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="688b3-129">Максимальная емкость (ГБ)</span><span class="sxs-lookup"><span data-stu-id="688b3-129">Maximum capacity (GB)</span></span> |<span data-ttu-id="688b3-130">500</span><span class="sxs-lookup"><span data-stu-id="688b3-130">500</span></span> |<span data-ttu-id="688b3-131">Общая емкость, могут быть использованы подписки в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-131">Total storage capacity that can be consumed by a subscription in this location.</span></span> |
| <span data-ttu-id="688b3-132">Общее число учетных записей хранения</span><span class="sxs-lookup"><span data-stu-id="688b3-132">Total number of storage accounts</span></span> |<span data-ttu-id="688b3-133">20</span><span class="sxs-lookup"><span data-stu-id="688b3-133">20</span></span> |<span data-ttu-id="688b3-134">Максимальное количество учетных записей хранилища, которые может создать подписки в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-134">The maximum number of storage accounts that a subscription can create in this location.</span></span> |

## <a name="network-quota-types"></a><span data-ttu-id="688b3-135">Типы квот сети</span><span class="sxs-lookup"><span data-stu-id="688b3-135">Network quota types</span></span>
| <span data-ttu-id="688b3-136">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="688b3-136">**Item**</span></span> | <span data-ttu-id="688b3-137">**Значение по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="688b3-137">**Default value**</span></span> | <span data-ttu-id="688b3-138">**Описание**</span><span class="sxs-lookup"><span data-stu-id="688b3-138">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="688b3-139">Max общедоступных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="688b3-139">Max public IPs</span></span> |<span data-ttu-id="688b3-140">50</span><span class="sxs-lookup"><span data-stu-id="688b3-140">50</span></span> |<span data-ttu-id="688b3-141">Максимальное число общих IP-адресов, можно создать подписки в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-141">The maximum number of public IPs that a subscription can create in this location.</span></span> |
| <span data-ttu-id="688b3-142">Max виртуальных сетей</span><span class="sxs-lookup"><span data-stu-id="688b3-142">Max virtual networks</span></span> |<span data-ttu-id="688b3-143">50</span><span class="sxs-lookup"><span data-stu-id="688b3-143">50</span></span> |<span data-ttu-id="688b3-144">Максимальное число виртуальных сетей, можно создать подписки в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-144">The maximum number of virtual networks that a subscription can create in this location.</span></span> |
| <span data-ttu-id="688b3-145">Max шлюзы виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="688b3-145">Max virtual network gateways</span></span> |<span data-ttu-id="688b3-146">1</span><span class="sxs-lookup"><span data-stu-id="688b3-146">1</span></span> |<span data-ttu-id="688b3-147">Максимальное число шлюзов виртуальной сети (VPN-шлюзов), которые можно создать подписки в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-147">The maximum number of virtual network gateways (VPN Gateways) that a subscription can create in this location.</span></span> |
| <span data-ttu-id="688b3-148">Максимум сетевых подключений</span><span class="sxs-lookup"><span data-stu-id="688b3-148">Max network connections</span></span> |<span data-ttu-id="688b3-149">2</span><span class="sxs-lookup"><span data-stu-id="688b3-149">2</span></span> |<span data-ttu-id="688b3-150">Максимальное количество сетевых подключений (point-to-point или сайт сайт), которые может создать подписку для всех шлюзов виртуальной сети в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-150">The maximum number of network connections (point-to-point or site-to-site) that a subscription can create across all virtual network gateways in this location.</span></span> |
| <span data-ttu-id="688b3-151">Max подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="688b3-151">Max load balancers</span></span> |<span data-ttu-id="688b3-152">50</span><span class="sxs-lookup"><span data-stu-id="688b3-152">50</span></span> |<span data-ttu-id="688b3-153">Максимальное число подсистем балансировки нагрузки, которые может создать подписки в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-153">The maximum number of load balancers that a subscription can create in this location.</span></span> |
| <span data-ttu-id="688b3-154">Максимальное число сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="688b3-154">Max NICs</span></span> |<span data-ttu-id="688b3-155">100</span><span class="sxs-lookup"><span data-stu-id="688b3-155">100</span></span> |<span data-ttu-id="688b3-156">Максимальное количество сетевых интерфейсов, которые можно создать подписки в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-156">The maximum number of network interfaces that a subscription can create in this location.</span></span> |
| <span data-ttu-id="688b3-157">Max Сетевые группы безопасности</span><span class="sxs-lookup"><span data-stu-id="688b3-157">Max network security groups</span></span> |<span data-ttu-id="688b3-158">50</span><span class="sxs-lookup"><span data-stu-id="688b3-158">50</span></span> |<span data-ttu-id="688b3-159">Максимальное число групп сетевой безопасности, которые можно создать подписки в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="688b3-159">The maximum number of network security groups that a subscription can create in this location.</span></span> |

## <a name="view-an-existing-quota"></a><span data-ttu-id="688b3-160">Просмотреть существующую квоту.</span><span class="sxs-lookup"><span data-stu-id="688b3-160">View an existing quota</span></span>
1. <span data-ttu-id="688b3-161">Нажмите кнопку **дополнительные службы** > **поставщиков ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="688b3-161">Click **More services** > **Resource Providers**.</span></span>
2. <span data-ttu-id="688b3-162">Выберите службу, квоту которого требуется просмотреть.</span><span class="sxs-lookup"><span data-stu-id="688b3-162">Select the service with the quota that you want to view.</span></span>
3. <span data-ttu-id="688b3-163">Нажмите кнопку **квоты**и установите квоты, требуется просмотреть.</span><span class="sxs-lookup"><span data-stu-id="688b3-163">Click **Quotas**, and select the quota you want to view.</span></span>

## <a name="next-steps"></a><span data-ttu-id="688b3-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="688b3-164">Next steps</span></span>
[<span data-ttu-id="688b3-165">Дополнительные сведения о планах, предложений и квоты.</span><span class="sxs-lookup"><span data-stu-id="688b3-165">Learn more about plans, offers, and quotas.</span></span>](azure-stack-plan-offer-quota-overview.md)

[<span data-ttu-id="688b3-166">Создание квоты при их создании.</span><span class="sxs-lookup"><span data-stu-id="688b3-166">Create quotas while creating a plan.</span></span>](azure-stack-create-plan.md)
