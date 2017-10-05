---
title: "Управление зонами DNS в службе DNS Azure с помощью PowerShell | Документация Майкрософт"
description: "Зонами DNS можно управлять с помощью Azure Powershell. В этой статье описывается, как обновлять, удалять и создавать зоны DNS в службе DNS Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 92f1da660d875c76d5d826669d6c1d12018c3d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-using-powershell"></a><span data-ttu-id="5fa80-104">Как управлять зонами DNS с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fa80-104">How to manage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5fa80-105">Портал</span><span class="sxs-lookup"><span data-stu-id="5fa80-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="5fa80-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fa80-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="5fa80-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5fa80-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="5fa80-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5fa80-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="5fa80-109">В этой статье описывается, как управлять зонами DNS с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fa80-109">This article shows you how to manage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="5fa80-110">Зонами DNS также можно управлять с помощью кроссплатформенного [интерфейса командной строки Azure](dns-operations-dnszones-cli.md) или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa80-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="5fa80-111">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="5fa80-111">Create a DNS zone</span></span>

<span data-ttu-id="5fa80-112">Зона DNS создается с помощью командлета `New-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="5fa80-112">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="5fa80-113">В следующем примере создается зона DNS *contoso.com* в группе ресурсов *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5fa80-113">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="5fa80-114">В следующем примере демонстрируется создание зоны DNS с двумя [тегами Azure Resource Manager](dns-zones-records.md#tags) (*project = demo* и *env = test*):</span><span class="sxs-lookup"><span data-stu-id="5fa80-114">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="5fa80-115">Получение зоны DNS</span><span class="sxs-lookup"><span data-stu-id="5fa80-115">Get a DNS zone</span></span>

<span data-ttu-id="5fa80-116">Чтобы получить зону DNS, используйте командлет `Get-AzureRmDnsZone` .</span><span class="sxs-lookup"><span data-stu-id="5fa80-116">To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="5fa80-117">Эта операция возвращает объект зоны DNS, соответствующий существующей зоне в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="5fa80-117">This operation returns a DNS zone object corresponding to an existing zone in Azure DNS.</span></span> <span data-ttu-id="5fa80-118">Объект содержит данные о зоне (например, число наборов записей), но не сами наборы записей (см. `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="5fa80-118">The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a><span data-ttu-id="5fa80-119">Перечисление зон DNS</span><span class="sxs-lookup"><span data-stu-id="5fa80-119">List DNS zones</span></span>

<span data-ttu-id="5fa80-120">Если опустить имя зоны в командлете `Get-AzureRmDnsZone`, можно получить список всех зон в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5fa80-120">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="5fa80-121">Эта операция возвращает массив объектов зоны.</span><span class="sxs-lookup"><span data-stu-id="5fa80-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="5fa80-122">Если опустить имя зоны и имя группы ресурсов в командлете `Get-AzureRmDnsZone`, то можно получить список всех зон в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa80-122">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="5fa80-123">Обновление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="5fa80-123">Update a DNS zone</span></span>

<span data-ttu-id="5fa80-124">Изменить ресурс зоны DNS можно с помощью командлета `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="5fa80-124">Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="5fa80-125">При этом ни один набор записей DNS в пределах зоны командлетом не обновляется (см. статью [Управление записями и наборами записей DNS с помощью PowerShell](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="5fa80-125">This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="5fa80-126">Эта команда используется только для обновления свойств самого ресурса зоны.</span><span class="sxs-lookup"><span data-stu-id="5fa80-126">It's only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="5fa80-127">В настоящее время к записываемым свойствам зоны относятся только [теги Azure Resource Manager для ресурса зоны](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="5fa80-127">The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="5fa80-128">Используйте один из двух описанных ниже способов обновления зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="5fa80-128">Use one of the following two ways to update a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a><span data-ttu-id="5fa80-129">Укажите зону с помощью имени и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5fa80-129">Specify the zone using the zone name and resource group</span></span>

<span data-ttu-id="5fa80-130">При этом подходе существующие теги зоны заменяются указанными значениями.</span><span class="sxs-lookup"><span data-stu-id="5fa80-130">This approach replaces the existing zone tags with the values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="5fa80-131">Укажите зону с помощью объекта $zone.</span><span class="sxs-lookup"><span data-stu-id="5fa80-131">Specify the zone using a $zone object</span></span>

<span data-ttu-id="5fa80-132">При этом подходе извлекается существующий объект зоны, изменяются теги, а затем фиксируются изменения.</span><span class="sxs-lookup"><span data-stu-id="5fa80-132">This approach retrieves the existing zone object, modifies the tags, and then commits the changes.</span></span> <span data-ttu-id="5fa80-133">Благодаря этому существующие теги могут сохраняться.</span><span class="sxs-lookup"><span data-stu-id="5fa80-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="5fa80-134">При использовании командлета `Set-AzureRmDnsZone` с объектом $zone применяются [проверки Etag](dns-zones-records.md#etags), чтобы параллельные изменения не были перезаписаны.</span><span class="sxs-lookup"><span data-stu-id="5fa80-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="5fa80-135">Чтобы отменить эти проверки, укажите необязательный параметр `-Overwrite`.</span><span class="sxs-lookup"><span data-stu-id="5fa80-135">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="5fa80-136">Удаление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="5fa80-136">Delete a DNS Zone</span></span>

<span data-ttu-id="5fa80-137">Зоны DNS можно удалить с помощью командлета `Remove-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="5fa80-137">DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="5fa80-138">При удалении зоны DNS также удаляются все записи DNS в этой зоне.</span><span class="sxs-lookup"><span data-stu-id="5fa80-138">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="5fa80-139">Эту операцию нельзя отменить.</span><span class="sxs-lookup"><span data-stu-id="5fa80-139">This operation cannot be undone.</span></span> <span data-ttu-id="5fa80-140">Если зона DNS используется, то после ее удаления произойдет сбой служб, которые ее используют.</span><span class="sxs-lookup"><span data-stu-id="5fa80-140">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="5fa80-141">Сведения о защите от случайного зоны удаления см. в разделе [How to protect DNS zones and records](dns-protect-zones-recordsets.md) (Как защитить зоны и записи DNS).</span><span class="sxs-lookup"><span data-stu-id="5fa80-141">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="5fa80-142">Используйте один из двух описанных ниже способов удаления зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="5fa80-142">Use one of the following two ways to delete a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a><span data-ttu-id="5fa80-143">Укажите зону с помощью имени зоны и имени группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5fa80-143">Specify the zone using the zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="5fa80-144">Укажите зону с помощью объекта $zone.</span><span class="sxs-lookup"><span data-stu-id="5fa80-144">Specify the zone using a $zone object</span></span>

<span data-ttu-id="5fa80-145">Удаляемую зону можно указать с помощью объекта `$zone`, который возвращается командлетом `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="5fa80-145">You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="5fa80-146">Объект зоны также можно направить в конвейер, а не передавать в качестве параметра:</span><span class="sxs-lookup"><span data-stu-id="5fa80-146">The zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="5fa80-147">Как и для командлета `Set-AzureRmDnsZone`, при указании набора записей с помощью объекта `$zone` вы включаете проверки Etag, чтобы убедиться, что параллельные изменения не удаляются.</span><span class="sxs-lookup"><span data-stu-id="5fa80-147">As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="5fa80-148">Чтобы отменить эти проверки, используйте параметр `-Overwrite`.</span><span class="sxs-lookup"><span data-stu-id="5fa80-148">Use the `-Overwrite` switch to suppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="5fa80-149">Запросы на подтверждение</span><span class="sxs-lookup"><span data-stu-id="5fa80-149">Confirmation prompts</span></span>

<span data-ttu-id="5fa80-150">Командлеты `New-AzureRmDnsZone`, `Set-AzureRmDnsZone` и `Remove-AzureRmDnsZone` поддерживают запросы на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="5fa80-150">The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="5fa80-151">Оба командлета (`New-AzureRmDnsZone` и `Set-AzureRmDnsZone`) запрашивают подтверждение, если привилегированная переменная `$ConfirmPreference` в PowerShell имеет значение `Medium` или ниже.</span><span class="sxs-lookup"><span data-stu-id="5fa80-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="5fa80-152">Из-за того, что удаление зоны DNS может иметь значительные последствия, командлет `Remove-AzureRmDnsZone` запрашивает подтверждение, если переменная PowerShell `$ConfirmPreference` имеет любое значение, отличное от `None`.</span><span class="sxs-lookup"><span data-stu-id="5fa80-152">Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="5fa80-153">Поскольку переменная `$ConfirmPreference` по умолчанию имеет значение `High`, то по умолчанию подтверждение запрашивается только командлетом `Remove-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="5fa80-153">Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="5fa80-154">Текущее значение `$ConfirmPreference` можно переопределить с помощью параметра `-Confirm`.</span><span class="sxs-lookup"><span data-stu-id="5fa80-154">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="5fa80-155">Если вы определите `-Confirm` или `-Confirm:$True`, командлет будет запрашивать подтверждение перед выполнением.</span><span class="sxs-lookup"><span data-stu-id="5fa80-155">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="5fa80-156">Если вы определите `-Confirm:$False`, командлет не будет запрашивать подтверждение.</span><span class="sxs-lookup"><span data-stu-id="5fa80-156">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="5fa80-157">Дополнительные сведения об элементах `-Confirm` и `$ConfirmPreference` см. в статье о [привилегированных переменных](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="5fa80-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fa80-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5fa80-158">Next steps</span></span>

<span data-ttu-id="5fa80-159">Узнайте, как [управлять наборами записей и записями](dns-operations-recordsets.md) в зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="5fa80-159">Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="5fa80-160">Узнайте, как [делегировать свой домен в Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="5fa80-160">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="5fa80-161">Просмотрите [справочную документацию по Azure DNS PowerShell](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="5fa80-161">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

