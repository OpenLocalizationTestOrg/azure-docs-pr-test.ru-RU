---
title: "aaaManage DNS-зоны в DNS Azure - портал Azure | Документы Microsoft"
description: "Можно управлять с помощью портала Azure hello зон DNS. В этой статье описывается, как tooupdate, удалите и создайте зон DNS на Azure DNS"
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
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a><span data-ttu-id="f5aab-104">Как toomanage зоны DNS в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f5aab-104">How toomanage DNS Zones in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5aab-105">Портал</span><span class="sxs-lookup"><span data-stu-id="f5aab-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="f5aab-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5aab-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="f5aab-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f5aab-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="f5aab-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f5aab-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="f5aab-109">В этой статье показано, как toomanage DNS-зоны с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f5aab-109">This article shows you how toomanage your DNS zones by using hello Azure portal.</span></span> <span data-ttu-id="f5aab-110">Также можно управлять с помощью hello кросс платформенных зон DNS [Azure CLI](dns-operations-dnszones-cli.md) или hello Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="f5aab-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="f5aab-111">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="f5aab-111">Create a DNS zone</span></span>

1. <span data-ttu-id="f5aab-112">Войдите в toohello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f5aab-112">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="f5aab-113">Hello концентратора меню и нажмите кнопку **Создать > Сетевые подключения >** и нажмите кнопку **зоны DNS** tooopen hello создать DNS-зоны колонку.</span><span class="sxs-lookup"><span data-stu-id="f5aab-113">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Зона DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="f5aab-115">На hello **создать DNS-зоны** колонки введите следующие значения hello, затем щелкните **создать**:</span><span class="sxs-lookup"><span data-stu-id="f5aab-115">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="f5aab-116">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="f5aab-116">**Setting**</span></span> | <span data-ttu-id="f5aab-117">**Значение**</span><span class="sxs-lookup"><span data-stu-id="f5aab-117">**Value**</span></span> | <span data-ttu-id="f5aab-118">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="f5aab-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="f5aab-119">**Имя**</span><span class="sxs-lookup"><span data-stu-id="f5aab-119">**Name**</span></span>|<span data-ttu-id="f5aab-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="f5aab-120">contoso.com</span></span>|<span data-ttu-id="f5aab-121">Имя зоны DNS hello Hello</span><span class="sxs-lookup"><span data-stu-id="f5aab-121">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="f5aab-122">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="f5aab-122">**Subscription**</span></span>|<span data-ttu-id="f5aab-123">[Ваша подписка]</span><span class="sxs-lookup"><span data-stu-id="f5aab-123">[Your subscription]</span></span>|<span data-ttu-id="f5aab-124">Выберите зону DNS toocreate hello подписки в.</span><span class="sxs-lookup"><span data-stu-id="f5aab-124">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="f5aab-125">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="f5aab-125">**Resource group**</span></span>|<span data-ttu-id="f5aab-126">**Создать:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="f5aab-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="f5aab-127">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f5aab-127">Create a resource group.</span></span> <span data-ttu-id="f5aab-128">Имя группы ресурсов Hello должно быть уникальным в пределах hello подписки, выбранной.</span><span class="sxs-lookup"><span data-stu-id="f5aab-128">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="f5aab-129">Дополнительные сведения о группах ресурсов, чтение hello toolearn [диспетчера ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) обзорную статью.</span><span class="sxs-lookup"><span data-stu-id="f5aab-129">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="f5aab-130">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="f5aab-130">**Location**</span></span>|<span data-ttu-id="f5aab-131">Запад США</span><span class="sxs-lookup"><span data-stu-id="f5aab-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="f5aab-132">Группа ресурсов Hello относится toohello расположение группы ресурсов hello, а не оказывает влияния на hello зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="f5aab-132">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="f5aab-133">расположение зоны DNS Hello всегда «глобальные» и не отображается.</span><span class="sxs-lookup"><span data-stu-id="f5aab-133">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="f5aab-134">Перечисление зон DNS</span><span class="sxs-lookup"><span data-stu-id="f5aab-134">List DNS zones</span></span>

<span data-ttu-id="f5aab-135">В hello портал Azure, перейдите в слишком**дополнительные службы** > **сети** > **зон DNS**.</span><span class="sxs-lookup"><span data-stu-id="f5aab-135">In hello Azure portal, navigate too**More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="f5aab-136">Каждая зона DNS является отдельным ресурсом. В этом представлении отображаются такие сведения, как число наборов записей и серверы имен.</span><span class="sxs-lookup"><span data-stu-id="f5aab-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="f5aab-137">столбец Hello **СЕРВЕРЫ ИМЕН** не находится в представлении по умолчанию hello tooadd его щелкните **столбцы**выберите **серверов имен** и нажмите кнопку **сделать**.</span><span class="sxs-lookup"><span data-stu-id="f5aab-137">hello column **NAME SERVERS** is not in hello default view, tooadd it click **Columns**, select **Name servers** and click **Done**.</span></span>

![Перечисление зон DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="f5aab-139">Удаление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="f5aab-139">Delete a DNS zone</span></span>

<span data-ttu-id="f5aab-140">Перейдите tooa зоны DNS в портале hello.</span><span class="sxs-lookup"><span data-stu-id="f5aab-140">Navigate tooa DNS zone in hello portal.</span></span> <span data-ttu-id="f5aab-141">На hello **зоны DNS** колонка, щелкните **удалить зону**.</span><span class="sxs-lookup"><span data-stu-id="f5aab-141">On hello **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="f5aab-142">Все запрашиваемые tooconfirm Желательное toodelete hello DNS-зоны.</span><span class="sxs-lookup"><span data-stu-id="f5aab-142">You are prompted tooconfirm you are wanting toodelete hello DNS zone.</span></span> <span data-ttu-id="f5aab-143">Зоны DNS при удалении также удаляются все записи hello, содержащихся в зоне hello.</span><span class="sxs-lookup"><span data-stu-id="f5aab-143">Deleting a DNS zone also deletes all hello records that are contained in hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5aab-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5aab-144">Next steps</span></span>

<span data-ttu-id="f5aab-145">Узнайте, как toowork с зоной DNS и записи, посетив [Приступая к работе с Azure DNS, с помощью портала Azure hello](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f5aab-145">Learn how toowork with your DNS Zone and records by visiting [Get started with Azure DNS using hello Azure portal](dns-getstarted-portal.md).</span></span>
