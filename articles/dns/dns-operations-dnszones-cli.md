---
title: "aaaManage DNS-зоны в DNS Azure - CLI Azure 2.0 | Документы Microsoft"
description: "Зонами DNS можно управлять с помощью Azure CLI 2.0. В этой статье показано, как tooupdate, удалите и создайте зон DNS на Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="67f7f-104">Как toomanage зоны DNS в Azure DNS с помощью hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="67f7f-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="67f7f-105">Портал</span><span class="sxs-lookup"><span data-stu-id="67f7f-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="67f7f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="67f7f-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="67f7f-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="67f7f-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="67f7f-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="67f7f-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="67f7f-109">В этом руководстве показано, как toomanage DNS-зоны с помощью hello кросс платформенных Azure CLI, который доступен для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="67f7f-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="67f7f-110">Также можно управлять с помощью зон DNS [Azure PowerShell](dns-operations-dnszones.md) или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="67f7f-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="67f7f-111">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="67f7f-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="67f7f-112">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="67f7f-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="67f7f-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -нашей CLI для hello классический и ресурса управления развертывания моделей.</span><span class="sxs-lookup"><span data-stu-id="67f7f-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="67f7f-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурса управления.</span><span class="sxs-lookup"><span data-stu-id="67f7f-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="67f7f-115">Введение</span><span class="sxs-lookup"><span data-stu-id="67f7f-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="67f7f-116">Настройка Azure CLI 2.0 для Azure DNS</span><span class="sxs-lookup"><span data-stu-id="67f7f-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="67f7f-117">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="67f7f-117">Before you begin</span></span>

<span data-ttu-id="67f7f-118">Проверьте наличие следующих элементов перед началом настройки hello.</span><span class="sxs-lookup"><span data-stu-id="67f7f-118">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="67f7f-119">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="67f7f-119">An Azure subscription.</span></span> <span data-ttu-id="67f7f-120">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67f7f-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="67f7f-121">Установить последнюю версию hello hello Azure 2.0 CLI, доступные для Windows, Linux или MAC.</span><span class="sxs-lookup"><span data-stu-id="67f7f-121">Install hello latest version of hello Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="67f7f-122">Дополнительные сведения можно найти по адресу [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="67f7f-122">More information is available at [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="67f7f-123">Войдите в tooyour учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="67f7f-123">Sign in tooyour Azure account</span></span>

<span data-ttu-id="67f7f-124">Откройте окно консоли и пройдите проверку подлинности с помощью своих учетных данных.</span><span class="sxs-lookup"><span data-stu-id="67f7f-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="67f7f-125">Дополнительные сведения см. в журнале в tooAzure из hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="67f7f-125">For more information, see Log in tooAzure from hello Azure CLI</span></span>

```
az login
```

### <a name="select-hello-subscription"></a><span data-ttu-id="67f7f-126">Выберите подписку hello</span><span class="sxs-lookup"><span data-stu-id="67f7f-126">Select hello subscription</span></span>

<span data-ttu-id="67f7f-127">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="67f7f-127">Check hello subscriptions for hello account.</span></span>

```
az account list
```

<span data-ttu-id="67f7f-128">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="67f7f-128">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="67f7f-129">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="67f7f-129">Create a resource group</span></span>

<span data-ttu-id="67f7f-130">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="67f7f-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="67f7f-131">Используется как расположение по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67f7f-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="67f7f-132">Тем не менее так как все ресурсы DNS глобального, не язык, выбор hello расположение группы ресурсов не оказывает влияния на Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="67f7f-132">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="67f7f-133">Если используется существующая группа ресурсов, можно пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="67f7f-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="67f7f-134">Получение справки</span><span class="sxs-lookup"><span data-stu-id="67f7f-134">Getting help</span></span>

<span data-ttu-id="67f7f-135">Все команды CLI 2.0, относящихся tooAzure DNS начинаются с `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-135">All CLI 2.0 commands relating tooAzure DNS start with `az network dns`.</span></span> <span data-ttu-id="67f7f-136">Справка доступна для каждой команды, с помощью hello `--help` параметр (Краткая форма `-h`).</span><span class="sxs-lookup"><span data-stu-id="67f7f-136">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="67f7f-137">Например:</span><span class="sxs-lookup"><span data-stu-id="67f7f-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="67f7f-138">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="67f7f-138">Create a DNS zone</span></span>

<span data-ttu-id="67f7f-139">Зоны DNS создается с помощью hello `az network dns zone create` команды.</span><span class="sxs-lookup"><span data-stu-id="67f7f-139">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="67f7f-140">Чтобы получить справку, см. `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="67f7f-141">Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello вызывается *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="67f7f-141">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="67f7f-142">toocreate зоны DNS с тегами</span><span class="sxs-lookup"><span data-stu-id="67f7f-142">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="67f7f-143">Hello следующем примере показано, как toocreate DNS зоны с двумя [диспетчера ресурсов Azure теги](dns-zones-records.md#tags), *проекта = Демонстрация* и *env = test*, с помощью hello `--tags` параметр (Краткая форма `-t`):</span><span class="sxs-lookup"><span data-stu-id="67f7f-143">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="67f7f-144">Получение зоны DNS</span><span class="sxs-lookup"><span data-stu-id="67f7f-144">Get a DNS zone</span></span>

<span data-ttu-id="67f7f-145">использовать tooretrieve зону DNS `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-145">tooretrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="67f7f-146">Чтобы получить справку, см. `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="67f7f-147">Hello следующий пример возвращает зоны DNS hello *contoso.com* и связанные с ним данные из группы ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="67f7f-147">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="67f7f-148">Следующий пример Hello — ответ hello.</span><span class="sxs-lookup"><span data-stu-id="67f7f-148">hello following example is hello response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="67f7f-149">Обратите внимание, что записи DNS не возвращаются командой `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="67f7f-150">toolist DNS-записи, используйте `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-150">toolist DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="67f7f-151">Перечисление зон DNS</span><span class="sxs-lookup"><span data-stu-id="67f7f-151">List DNS zones</span></span>

<span data-ttu-id="67f7f-152">использовать tooenumerate зон DNS, `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-152">tooenumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="67f7f-153">Чтобы получить справку, см. `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="67f7f-154">Указание группы ресурсов hello перечислены только те зоны в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="67f7f-154">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="67f7f-155">Пропуск группы ресурсов hello список всех зон в подписке hello:</span><span class="sxs-lookup"><span data-stu-id="67f7f-155">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="67f7f-156">Обновление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="67f7f-156">Update a DNS zone</span></span>

<span data-ttu-id="67f7f-157">Изменения tooa ресурсов зоны DNS можно при помощи `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-157">Changes tooa DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="67f7f-158">Чтобы получить справку, см. `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="67f7f-159">Эта команда не обновляет hello наборы записей DNS в зоне hello (см. [как DNS-записи tooManage](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="67f7f-159">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="67f7f-160">Это свойства только используемые tooupdate сам ресурс hello зоны.</span><span class="sxs-lookup"><span data-stu-id="67f7f-160">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="67f7f-161">Эти свойства доступны в настоящее время составляет toohello [диспетчера ресурсов Azure «теги»](dns-zones-records.md#tags) для ресурса зоны hello.</span><span class="sxs-lookup"><span data-stu-id="67f7f-161">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="67f7f-162">Hello следующем примере показано, как tooupdate hello тегов в зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="67f7f-162">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="67f7f-163">существующие теги Hello заменяются указано значение hello.</span><span class="sxs-lookup"><span data-stu-id="67f7f-163">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="67f7f-164">Удаление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="67f7f-164">Delete a DNS zone</span></span>

<span data-ttu-id="67f7f-165">Зоны DNS можно удалить с помощью команды `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="67f7f-166">Чтобы получить справку, см. `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="67f7f-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="67f7f-167">Зоны DNS при удалении также удаляются все записи DNS в зоне hello.</span><span class="sxs-lookup"><span data-stu-id="67f7f-167">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="67f7f-168">Эту операцию нельзя отменить.</span><span class="sxs-lookup"><span data-stu-id="67f7f-168">This operation cannot be undone.</span></span> <span data-ttu-id="67f7f-169">Если зона DNS hello, службы, используя зоны hello сможет hello зона удаляется.</span><span class="sxs-lookup"><span data-stu-id="67f7f-169">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="67f7f-170">tooprotect от зоны случайного удаления, в разделе [как tooprotect DNS-зоны и записывает](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="67f7f-170">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="67f7f-171">Эта команда запрашивает подтверждение.</span><span class="sxs-lookup"><span data-stu-id="67f7f-171">This command prompts for confirmation.</span></span> <span data-ttu-id="67f7f-172">Необязательный Hello `--yes` подавляет этот запрос.</span><span class="sxs-lookup"><span data-stu-id="67f7f-172">hello optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="67f7f-173">Hello следующем примере показано, как toodelete hello зоны *contoso.com* из группы ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="67f7f-173">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="67f7f-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="67f7f-174">Next steps</span></span>

<span data-ttu-id="67f7f-175">Узнайте, каким образом слишком[управления наборов записей и записи](dns-getstarted-create-recordset-cli.md) в зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="67f7f-175">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="67f7f-176">Узнайте, каким образом слишком[делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="67f7f-176">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

