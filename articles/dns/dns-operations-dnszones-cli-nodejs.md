---
title: "aaaManage DNS-зоны в DNS Azure - Azure CLI 1.0 | Документы Microsoft"
description: "Зонами DNS можно управлять с помощью Azure CLI 1.0. В этой статье показано, как tooupdate, удалите и создайте зон DNS на Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="7ca11-104">Как toomanage зоны DNS в Azure DNS с помощью hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7ca11-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ca11-105">Портал</span><span class="sxs-lookup"><span data-stu-id="7ca11-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="7ca11-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ca11-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="7ca11-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7ca11-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="7ca11-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7ca11-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="7ca11-109">В этом руководстве показано, как toomanage DNS-зоны с помощью hello кросс платформенных Azure CLI 1.0, которая доступна для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="7ca11-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="7ca11-110">Также можно управлять с помощью зон DNS [Azure PowerShell](dns-operations-dnszones.md) или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7ca11-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="7ca11-111">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="7ca11-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="7ca11-112">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="7ca11-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="7ca11-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -нашей CLI для hello классический и ресурса управления развертывания моделей.</span><span class="sxs-lookup"><span data-stu-id="7ca11-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="7ca11-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурса управления.</span><span class="sxs-lookup"><span data-stu-id="7ca11-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="7ca11-115">Введение</span><span class="sxs-lookup"><span data-stu-id="7ca11-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="7ca11-116">Получение справки</span><span class="sxs-lookup"><span data-stu-id="7ca11-116">Getting help</span></span>

<span data-ttu-id="7ca11-117">Все команды CLI 1.0 связанные tooAzure DNS начинаются с `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-117">All CLI 1.0 commands relating tooAzure DNS start with `azure network dns`.</span></span> <span data-ttu-id="7ca11-118">Справка доступна для каждой команды, с помощью hello `--help` параметр (Краткая форма `-h`).</span><span class="sxs-lookup"><span data-stu-id="7ca11-118">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="7ca11-119">Например:</span><span class="sxs-lookup"><span data-stu-id="7ca11-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="7ca11-120">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="7ca11-120">Create a DNS zone</span></span>

<span data-ttu-id="7ca11-121">Зоны DNS создается с помощью hello `azure network dns zone create` команды.</span><span class="sxs-lookup"><span data-stu-id="7ca11-121">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="7ca11-122">Чтобы получить справку, см. `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="7ca11-123">Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello вызывается *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="7ca11-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="7ca11-124">toocreate зоны DNS с тегами</span><span class="sxs-lookup"><span data-stu-id="7ca11-124">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="7ca11-125">Hello следующем примере показано, как toocreate DNS зоны с двумя [диспетчера ресурсов Azure теги](dns-zones-records.md#tags), *проекта = Демонстрация* и *env = test*, с помощью hello `--tags` параметр (Краткая форма `-t`):</span><span class="sxs-lookup"><span data-stu-id="7ca11-125">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="7ca11-126">Получение зоны DNS</span><span class="sxs-lookup"><span data-stu-id="7ca11-126">Get a DNS zone</span></span>

<span data-ttu-id="7ca11-127">использовать tooretrieve зону DNS `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-127">tooretrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="7ca11-128">Чтобы получить справку, см. `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="7ca11-129">Hello следующий пример возвращает зоны DNS hello *contoso.com* и связанные с ним данные из группы ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7ca11-129">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="7ca11-130">Следующий пример Hello — ответ hello.</span><span class="sxs-lookup"><span data-stu-id="7ca11-130">hello following example is hello response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

<span data-ttu-id="7ca11-131">Обратите внимание, что записи DNS не возвращаются командой `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="7ca11-132">toolist DNS-записи, используйте `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-132">toolist DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="7ca11-133">Перечисление зон DNS</span><span class="sxs-lookup"><span data-stu-id="7ca11-133">List DNS zones</span></span>

<span data-ttu-id="7ca11-134">использовать tooenumerate зон DNS, `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-134">tooenumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="7ca11-135">Чтобы получить справку, см. `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="7ca11-136">Указание группы ресурсов hello перечислены только те зоны в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="7ca11-136">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="7ca11-137">Пропуск группы ресурсов hello список всех зон в подписке hello:</span><span class="sxs-lookup"><span data-stu-id="7ca11-137">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="7ca11-138">Обновление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="7ca11-138">Update a DNS zone</span></span>

<span data-ttu-id="7ca11-139">Изменения tooa ресурсов зоны DNS можно при помощи `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-139">Changes tooa DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="7ca11-140">Чтобы получить справку, см. `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="7ca11-141">Эта команда не обновляет hello наборы записей DNS в зоне hello (см. [как DNS-записи tooManage](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="7ca11-141">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="7ca11-142">Это свойства только используемые tooupdate сам ресурс hello зоны.</span><span class="sxs-lookup"><span data-stu-id="7ca11-142">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="7ca11-143">Эти свойства доступны в настоящее время составляет toohello [диспетчера ресурсов Azure «теги»](dns-zones-records.md#tags) для ресурса зоны hello.</span><span class="sxs-lookup"><span data-stu-id="7ca11-143">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="7ca11-144">Hello следующем примере показано, как tooupdate hello тегов в зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="7ca11-144">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="7ca11-145">существующие теги Hello заменяются указано значение hello.</span><span class="sxs-lookup"><span data-stu-id="7ca11-145">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="7ca11-146">Удаление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="7ca11-146">Delete a DNS Zone</span></span>

<span data-ttu-id="7ca11-147">Зоны DNS можно удалить с помощью команды `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="7ca11-148">Чтобы получить справку, см. `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="7ca11-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="7ca11-149">Зоны DNS при удалении также удаляются все записи DNS в зоне hello.</span><span class="sxs-lookup"><span data-stu-id="7ca11-149">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="7ca11-150">Эту операцию нельзя отменить.</span><span class="sxs-lookup"><span data-stu-id="7ca11-150">This operation cannot be undone.</span></span> <span data-ttu-id="7ca11-151">Если зона DNS hello, службы, используя зоны hello сможет hello зона удаляется.</span><span class="sxs-lookup"><span data-stu-id="7ca11-151">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="7ca11-152">tooprotect от зоны случайного удаления, в разделе [как tooprotect DNS-зоны и записывает](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="7ca11-152">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="7ca11-153">Эта команда запрашивает подтверждение.</span><span class="sxs-lookup"><span data-stu-id="7ca11-153">This command prompts for confirmation.</span></span> <span data-ttu-id="7ca11-154">Необязательный Hello `--quiet` переключения (Краткая форма `-q`) отключает это предупреждение.</span><span class="sxs-lookup"><span data-stu-id="7ca11-154">hello optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="7ca11-155">Hello следующем примере показано, как toodelete hello зоны *contoso.com* из группы ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7ca11-155">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="7ca11-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ca11-156">Next steps</span></span>

<span data-ttu-id="7ca11-157">Узнайте, каким образом слишком[управления наборов записей и записи](dns-getstarted-create-recordset-cli-nodejs.md) в зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="7ca11-157">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="7ca11-158">Узнайте, каким образом слишком[делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="7ca11-158">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

