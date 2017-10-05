---
title: "Управление зонами DNS в службе DNS Azure (Azure CLI 2.0) | Документация Майкрософт"
description: "Зонами DNS можно управлять с помощью Azure CLI 2.0. В этой статье показано, как обновлять, удалять и создавать зоны DNS в службе DNS Azure."
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
ms.openlocfilehash: 1414baf9e51d648cc3a46c4f8635040b4d276910
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="468a8-104">Как управлять зонами DNS в службе DNS Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="468a8-104">How to manage DNS Zones in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="468a8-105">Портал</span><span class="sxs-lookup"><span data-stu-id="468a8-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="468a8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="468a8-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="468a8-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="468a8-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="468a8-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="468a8-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="468a8-109">В этом руководстве показано, как управлять зонами DNS с помощью кроссплатформенного интерфейса командной строки Azure, доступного для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="468a8-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="468a8-110">Зонами DNS также можно управлять с помощью [Azure PowerShell](dns-operations-dnszones.md) или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="468a8-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="468a8-111">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="468a8-111">CLI versions to complete the task</span></span>

<span data-ttu-id="468a8-112">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="468a8-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="468a8-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) — это интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="468a8-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="468a8-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) — это интерфейс командной строки нового поколения для модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="468a8-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="468a8-115">Введение</span><span class="sxs-lookup"><span data-stu-id="468a8-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="468a8-116">Настройка Azure CLI 2.0 для Azure DNS</span><span class="sxs-lookup"><span data-stu-id="468a8-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="468a8-117">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="468a8-117">Before you begin</span></span>

<span data-ttu-id="468a8-118">Перед началом настройки убедитесь, что у вас есть следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="468a8-118">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="468a8-119">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="468a8-119">An Azure subscription.</span></span> <span data-ttu-id="468a8-120">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="468a8-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="468a8-121">Установите последнюю версию Azure CLI 2.0 для Windows, Linux или Mac.</span><span class="sxs-lookup"><span data-stu-id="468a8-121">Install the latest version of the Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="468a8-122">Дополнительные сведения см. в статье [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2) (Установка Azure CLI 2.0).</span><span class="sxs-lookup"><span data-stu-id="468a8-122">More information is available at [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="468a8-123">Вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="468a8-123">Sign in to your Azure account</span></span>

<span data-ttu-id="468a8-124">Откройте окно консоли и пройдите проверку подлинности с помощью своих учетных данных.</span><span class="sxs-lookup"><span data-stu-id="468a8-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="468a8-125">Дополнительные сведения см. в статье "Вход в Azure из командной строки Azure".</span><span class="sxs-lookup"><span data-stu-id="468a8-125">For more information, see Log in to Azure from the Azure CLI</span></span>

```
az login
```

### <a name="select-the-subscription"></a><span data-ttu-id="468a8-126">Выбор подписки</span><span class="sxs-lookup"><span data-stu-id="468a8-126">Select the subscription</span></span>

<span data-ttu-id="468a8-127">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="468a8-127">Check the subscriptions for the account.</span></span>

```
az account list
```

<span data-ttu-id="468a8-128">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="468a8-128">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="468a8-129">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="468a8-129">Create a resource group</span></span>

<span data-ttu-id="468a8-130">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="468a8-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="468a8-131">Оно используется в качестве расположения по умолчанию для всех ресурсов данной группы.</span><span class="sxs-lookup"><span data-stu-id="468a8-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="468a8-132">Но так как все ресурсы DNS глобальные, а не региональные, выбор расположения группы ресурсов не влияет на Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="468a8-132">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="468a8-133">Если используется существующая группа ресурсов, можно пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="468a8-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="468a8-134">Получение справки</span><span class="sxs-lookup"><span data-stu-id="468a8-134">Getting help</span></span>

<span data-ttu-id="468a8-135">Все команды CLI 2.0 для Azure DNS начинаются с `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="468a8-135">All CLI 2.0 commands relating to Azure DNS start with `az network dns`.</span></span> <span data-ttu-id="468a8-136">Справку для каждой команды можно отобразить с помощью параметра `--help` (краткая форма: `-h`).</span><span class="sxs-lookup"><span data-stu-id="468a8-136">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="468a8-137">Например:</span><span class="sxs-lookup"><span data-stu-id="468a8-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="468a8-138">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="468a8-138">Create a DNS zone</span></span>

<span data-ttu-id="468a8-139">Зона DNS создается с помощью команды `az network dns zone create`.</span><span class="sxs-lookup"><span data-stu-id="468a8-139">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="468a8-140">Чтобы получить справку, см. `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="468a8-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="468a8-141">В следующем примере создается зона DNS *contoso.com* в группе ресурсов *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="468a8-141">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="468a8-142">Создание зоны DNS с тегами</span><span class="sxs-lookup"><span data-stu-id="468a8-142">To create a DNS zone with tags</span></span>

<span data-ttu-id="468a8-143">В следующем примере демонстрируется создание зоны DNS с двумя [тегами Azure Resource Manager](dns-zones-records.md#tags) (*project = demo* и *env = test*) с помощью параметра `--tags` (краткая форма: `-t`):</span><span class="sxs-lookup"><span data-stu-id="468a8-143">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="468a8-144">Получение зоны DNS</span><span class="sxs-lookup"><span data-stu-id="468a8-144">Get a DNS zone</span></span>

<span data-ttu-id="468a8-145">Чтобы получить зону DNS, используйте команду `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="468a8-145">To retrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="468a8-146">Чтобы получить справку, см. `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="468a8-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="468a8-147">В следующем примере возвращается зона DNS *contoso.com* и связанные с ней данные из группы ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="468a8-147">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="468a8-148">Ниже приведен пример ответа.</span><span class="sxs-lookup"><span data-stu-id="468a8-148">The following example is the response.</span></span>

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

<span data-ttu-id="468a8-149">Обратите внимание, что записи DNS не возвращаются командой `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="468a8-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="468a8-150">Для вывода списка записей DNS используйте `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="468a8-150">To list DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="468a8-151">Перечисление зон DNS</span><span class="sxs-lookup"><span data-stu-id="468a8-151">List DNS zones</span></span>

<span data-ttu-id="468a8-152">Чтобы перечислить зоны DNS, используйте `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="468a8-152">To enumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="468a8-153">Чтобы получить справку, см. `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="468a8-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="468a8-154">Если указать группу ресурсов, то будут перечислены только зоны в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="468a8-154">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="468a8-155">Если не указать группу ресурсов, то будут перечислены все зоны в подписке.</span><span class="sxs-lookup"><span data-stu-id="468a8-155">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="468a8-156">Обновление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="468a8-156">Update a DNS zone</span></span>

<span data-ttu-id="468a8-157">Изменить ресурс зоны DNS можно с помощью командлета `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="468a8-157">Changes to a DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="468a8-158">Чтобы получить справку, см. `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="468a8-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="468a8-159">Это команда не обновляет ни один набор записей DNS в пределах зоны (прочитайте статью [Управление записями и наборами записей DNS с помощью PowerShell](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="468a8-159">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="468a8-160">Эта команда используется только для обновления свойств самого ресурса зоны.</span><span class="sxs-lookup"><span data-stu-id="468a8-160">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="468a8-161">В настоящее время к этим свойствам относятся только [теги Azure Resource Manager](dns-zones-records.md#tags) для ресурса зоны.</span><span class="sxs-lookup"><span data-stu-id="468a8-161">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="468a8-162">В приведенном ниже примере показано, как обновить теги для зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="468a8-162">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="468a8-163">Существующие теги заменяются указанным значением.</span><span class="sxs-lookup"><span data-stu-id="468a8-163">The existing tags are replaced by the value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="468a8-164">Удаление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="468a8-164">Delete a DNS zone</span></span>

<span data-ttu-id="468a8-165">Зоны DNS можно удалить с помощью команды `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="468a8-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="468a8-166">Чтобы получить справку, см. `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="468a8-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="468a8-167">При удалении зоны DNS также удаляются все записи DNS в этой зоне.</span><span class="sxs-lookup"><span data-stu-id="468a8-167">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="468a8-168">Эту операцию нельзя отменить.</span><span class="sxs-lookup"><span data-stu-id="468a8-168">This operation cannot be undone.</span></span> <span data-ttu-id="468a8-169">Если зона DNS используется, то после ее удаления произойдет сбой служб, которые ее используют.</span><span class="sxs-lookup"><span data-stu-id="468a8-169">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="468a8-170">Сведения о защите от случайного зоны удаления см. в разделе [How to protect DNS zones and records](dns-protect-zones-recordsets.md) (Как защитить зоны и записи DNS).</span><span class="sxs-lookup"><span data-stu-id="468a8-170">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="468a8-171">Эта команда запрашивает подтверждение.</span><span class="sxs-lookup"><span data-stu-id="468a8-171">This command prompts for confirmation.</span></span> <span data-ttu-id="468a8-172">Необязательный параметр `--yes` позволяет отключить этот запрос.</span><span class="sxs-lookup"><span data-stu-id="468a8-172">The optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="468a8-173">В следующем примере показано, как удалить зону *contoso.com* из группы ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="468a8-173">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="468a8-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="468a8-174">Next steps</span></span>

<span data-ttu-id="468a8-175">Узнайте, как [управлять наборами записей и записями](dns-getstarted-create-recordset-cli.md) в зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="468a8-175">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="468a8-176">Узнайте, как [делегировать свой домен в Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="468a8-176">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

