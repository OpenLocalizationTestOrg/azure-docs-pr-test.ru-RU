---
title: "Управление зонами DNS в службе DNS Azure — портал Azure | Документация Майкрософт"
description: "Зонами DNS можно управлять с помощью портала Azure. В этой статье описывается, как обновлять, удалять и создавать зоны DNS в службе DNS Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 69a509612e6204fc93dd42bf2fe69cb165b5777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-the-azure-portal"></a><span data-ttu-id="12fcf-104">Как управлять зонами DNS с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="12fcf-104">How to manage DNS Zones in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="12fcf-105">Портал</span><span class="sxs-lookup"><span data-stu-id="12fcf-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="12fcf-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12fcf-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="12fcf-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="12fcf-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="12fcf-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="12fcf-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="12fcf-109">В этой статье объясняется, как управлять зонами DNS с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="12fcf-109">This article shows you how to manage your DNS zones by using the Azure portal.</span></span> <span data-ttu-id="12fcf-110">Зонами DNS также можно управлять с помощью кроссплатформенного [Azure CLI](dns-operations-dnszones-cli.md) или Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="12fcf-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="12fcf-111">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="12fcf-111">Create a DNS zone</span></span>

1. <span data-ttu-id="12fcf-112">Выполните вход на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="12fcf-112">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="12fcf-113">В главном меню щелкните **Создать > Сети**, а затем щелкните **Зона DNS**, чтобы открыть колонку "Создать зону DNS".</span><span class="sxs-lookup"><span data-stu-id="12fcf-113">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Зона DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="12fcf-115">В колонке **Создание зоны DNS** введите следующие значения, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="12fcf-115">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="12fcf-116">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="12fcf-116">**Setting**</span></span> | <span data-ttu-id="12fcf-117">**Значение**</span><span class="sxs-lookup"><span data-stu-id="12fcf-117">**Value**</span></span> | <span data-ttu-id="12fcf-118">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="12fcf-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="12fcf-119">**Имя**</span><span class="sxs-lookup"><span data-stu-id="12fcf-119">**Name**</span></span>|<span data-ttu-id="12fcf-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="12fcf-120">contoso.com</span></span>|<span data-ttu-id="12fcf-121">Имя зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="12fcf-121">The name of the DNS zone</span></span>|
   |<span data-ttu-id="12fcf-122">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="12fcf-122">**Subscription**</span></span>|<span data-ttu-id="12fcf-123">[Ваша подписка]</span><span class="sxs-lookup"><span data-stu-id="12fcf-123">[Your subscription]</span></span>|<span data-ttu-id="12fcf-124">Выберите подписку для создания зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="12fcf-124">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="12fcf-125">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="12fcf-125">**Resource group**</span></span>|<span data-ttu-id="12fcf-126">**Создать:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="12fcf-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="12fcf-127">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="12fcf-127">Create a resource group.</span></span> <span data-ttu-id="12fcf-128">Имя группы ресурсов должно быть уникальным в пределах выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="12fcf-128">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="12fcf-129">Дополнительные сведения о группах ресурсов см. в разделе [Группы ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) статьи "Общие сведения об Azure Resource Manager".</span><span class="sxs-lookup"><span data-stu-id="12fcf-129">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="12fcf-130">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="12fcf-130">**Location**</span></span>|<span data-ttu-id="12fcf-131">Запад США</span><span class="sxs-lookup"><span data-stu-id="12fcf-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="12fcf-132">Этот параметр относится к расположению группы ресурсов и никак не влияет на расположение зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="12fcf-132">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="12fcf-133">Расположение зоны DNS всегда является "глобальным" и не отображается.</span><span class="sxs-lookup"><span data-stu-id="12fcf-133">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="12fcf-134">Перечисление зон DNS</span><span class="sxs-lookup"><span data-stu-id="12fcf-134">List DNS zones</span></span>

<span data-ttu-id="12fcf-135">На портале Azure последовательно выберите **Больше служб** > **Сети** > **Зоны DNS**.</span><span class="sxs-lookup"><span data-stu-id="12fcf-135">In the Azure portal, navigate to **More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="12fcf-136">Каждая зона DNS является отдельным ресурсом. В этом представлении отображаются такие сведения, как число наборов записей и серверы имен.</span><span class="sxs-lookup"><span data-stu-id="12fcf-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="12fcf-137">Столбец **Серверы имен** не отображается в представлении по умолчанию. Чтобы добавить его, щелкните **Столбцы**, выберите **Серверы имен** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="12fcf-137">The column **NAME SERVERS** is not in the default view, to add it click **Columns**, select **Name servers** and click **Done**.</span></span>

![Перечисление зон DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="12fcf-139">Удаление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="12fcf-139">Delete a DNS zone</span></span>

<span data-ttu-id="12fcf-140">Перейдите к зоне DNS на портале.</span><span class="sxs-lookup"><span data-stu-id="12fcf-140">Navigate to a DNS zone in the portal.</span></span> <span data-ttu-id="12fcf-141">В колонке **Зона DNS** щелкните **Удалить зону**.</span><span class="sxs-lookup"><span data-stu-id="12fcf-141">On the **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="12fcf-142">Отобразится запрос на подтверждение удаления зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="12fcf-142">You are prompted to confirm you are wanting to delete the DNS zone.</span></span> <span data-ttu-id="12fcf-143">При удалении зоны DNS также удаляются все записи, которые содержатся в ней.</span><span class="sxs-lookup"><span data-stu-id="12fcf-143">Deleting a DNS zone also deletes all the records that are contained in the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12fcf-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12fcf-144">Next steps</span></span>

<span data-ttu-id="12fcf-145">Сведения о работе с зоной и записями DNS см. в статье [Приступая к работе со службой DNS Azure с помощью портала Azure](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="12fcf-145">Learn how to work with your DNS Zone and records by visiting [Get started with Azure DNS using the Azure portal](dns-getstarted-portal.md).</span></span>