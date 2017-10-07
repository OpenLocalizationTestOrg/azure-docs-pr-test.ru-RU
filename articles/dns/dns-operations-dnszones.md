---
title: "aaaManage DNS-зоны в Azure DNS - PowerShell | Документы Microsoft"
description: "Зонами DNS можно управлять с помощью Azure Powershell. В этой статье описывается, как tooupdate, удалите и создайте зон DNS на Azure DNS"
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
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a><span data-ttu-id="09747-104">Как toomanage зон DNS, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="09747-104">How toomanage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="09747-105">Портал</span><span class="sxs-lookup"><span data-stu-id="09747-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="09747-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="09747-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="09747-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="09747-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="09747-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="09747-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="09747-109">В этой статье показано, как toomanage DNS-зоны с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09747-109">This article shows you how toomanage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="09747-110">Также можно управлять с помощью hello кросс платформенных зон DNS [Azure CLI](dns-operations-dnszones-cli.md) или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="09747-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="09747-111">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="09747-111">Create a DNS zone</span></span>

<span data-ttu-id="09747-112">Зоны DNS создается с помощью hello `New-AzureRmDnsZone` командлета.</span><span class="sxs-lookup"><span data-stu-id="09747-112">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="09747-113">Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello вызывается *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="09747-113">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="09747-114">Hello следующем примере показано, как toocreate DNS зоны с двумя [диспетчера ресурсов Azure теги](dns-zones-records.md#tags), *проекта = Демонстрация* и *env = test*:</span><span class="sxs-lookup"><span data-stu-id="09747-114">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="09747-115">Получение зоны DNS</span><span class="sxs-lookup"><span data-stu-id="09747-115">Get a DNS zone</span></span>

<span data-ttu-id="09747-116">tooretrieve зоны DNS, используйте hello `Get-AzureRmDnsZone` командлета.</span><span class="sxs-lookup"><span data-stu-id="09747-116">tooretrieve a DNS zone, use hello `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="09747-117">Эта операция возвращает объект соответствующего tooan существующей зоны в Azure DNS зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="09747-117">This operation returns a DNS zone object corresponding tooan existing zone in Azure DNS.</span></span> <span data-ttu-id="09747-118">Hello объекта содержит данные о зоне hello (например hello число наборов записей), но не содержит наборы записей hello сами (см. `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="09747-118">hello object contains data about hello zone (such as hello number of record sets), but does not contain hello record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

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

## <a name="list-dns-zones"></a><span data-ttu-id="09747-119">Перечисление зон DNS</span><span class="sxs-lookup"><span data-stu-id="09747-119">List DNS zones</span></span>

<span data-ttu-id="09747-120">Имя зоны hello из `Get-AzureRmDnsZone`, можно перечислить все зоны в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="09747-120">By omitting hello zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="09747-121">Эта операция возвращает массив объектов зоны.</span><span class="sxs-lookup"><span data-stu-id="09747-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="09747-122">Не указывайте имя зоны hello и имя группы ресурсов hello из `Get-AzureRmDnsZone`, можно перечислить все зоны в hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="09747-122">By omitting both hello zone name and hello resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in hello Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="09747-123">Обновление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="09747-123">Update a DNS zone</span></span>

<span data-ttu-id="09747-124">Изменения ресурсов зоны DNS можно сделать с помощью tooa `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="09747-124">Changes tooa DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="09747-125">Этот командлет не обновляет hello наборы записей DNS в зоне hello (см. [как DNS-записи tooManage](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="09747-125">This cmdlet does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="09747-126">Только свойства tooupdate сам ресурс hello зоны.</span><span class="sxs-lookup"><span data-stu-id="09747-126">It's only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="09747-127">свойства для записи зоны Hello, в настоящее время составляет toohello [диспетчера ресурсов Azure «теги» для ресурса зоны hello](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="09747-127">hello writable zone properties are currently limited toohello [Azure Resource Manager ‘tags’ for hello zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="09747-128">Используйте один из следующих двух способов tooupdate hello зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="09747-128">Use one of hello following two ways tooupdate a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a><span data-ttu-id="09747-129">Укажите hello зоны с помощью hello зоны имя и группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="09747-129">Specify hello zone using hello zone name and resource group</span></span>

<span data-ttu-id="09747-130">Этот подход заменяет существующие теги зоны hello значениями hello.</span><span class="sxs-lookup"><span data-stu-id="09747-130">This approach replaces hello existing zone tags with hello values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="09747-131">Укажите hello зоны с помощью объекта $zone</span><span class="sxs-lookup"><span data-stu-id="09747-131">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="09747-132">Этот подход извлекает существующий объект зоны hello, изменяющий теги hello и затем фиксирует изменения hello.</span><span class="sxs-lookup"><span data-stu-id="09747-132">This approach retrieves hello existing zone object, modifies hello tags, and then commits hello changes.</span></span> <span data-ttu-id="09747-133">Благодаря этому существующие теги могут сохраняться.</span><span class="sxs-lookup"><span data-stu-id="09747-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="09747-134">При использовании `Set-AzureRmDnsZone` с объектом $zone [проверяет Etag](dns-zones-records.md#etags) используются tooensure параллельных изменений не перезаписываются.</span><span class="sxs-lookup"><span data-stu-id="09747-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="09747-135">Можно использовать необязательный hello `-Overwrite` переключения toosuppress этих проверок.</span><span class="sxs-lookup"><span data-stu-id="09747-135">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="09747-136">Удаление зоны DNS</span><span class="sxs-lookup"><span data-stu-id="09747-136">Delete a DNS Zone</span></span>

<span data-ttu-id="09747-137">Зоны DNS-сервера могут быть удалены с помощью hello `Remove-AzureRmDnsZone` командлета.</span><span class="sxs-lookup"><span data-stu-id="09747-137">DNS zones can be deleted using hello `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="09747-138">Зоны DNS при удалении также удаляются все записи DNS в зоне hello.</span><span class="sxs-lookup"><span data-stu-id="09747-138">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="09747-139">Эту операцию нельзя отменить.</span><span class="sxs-lookup"><span data-stu-id="09747-139">This operation cannot be undone.</span></span> <span data-ttu-id="09747-140">Если зона DNS hello, службы, используя зоны hello сможет hello зона удаляется.</span><span class="sxs-lookup"><span data-stu-id="09747-140">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="09747-141">tooprotect от зоны случайного удаления, в разделе [как tooprotect DNS-зоны и записывает](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="09747-141">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="09747-142">Используйте один из следующих двух способов toodelete hello зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="09747-142">Use one of hello following two ways toodelete a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a><span data-ttu-id="09747-143">Укажите hello зоны с помощью имени зоны hello и имя группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="09747-143">Specify hello zone using hello zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="09747-144">Укажите hello зоны с помощью объекта $zone</span><span class="sxs-lookup"><span data-stu-id="09747-144">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="09747-145">Можно указать toobe зоны hello, удаляются с помощью `$zone` объект, возвращаемый `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="09747-145">You can specify hello zone toobe deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="09747-146">Hello объекта зоны также можно направить вместо передан в качестве параметра:</span><span class="sxs-lookup"><span data-stu-id="09747-146">hello zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="09747-147">Как и в `Set-AzureRmDnsZone`, указав hello зоны с помощью `$zone` объекта включает Etag проверяет tooensure параллельных изменений не удаляются.</span><span class="sxs-lookup"><span data-stu-id="09747-147">As with `Set-AzureRmDnsZone`, specifying hello zone using a `$zone` object enables Etag checks tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="09747-148">Используйте hello `-Overwrite` переключения toosuppress этих проверок.</span><span class="sxs-lookup"><span data-stu-id="09747-148">Use hello `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="09747-149">Запросы на подтверждение</span><span class="sxs-lookup"><span data-stu-id="09747-149">Confirmation prompts</span></span>

<span data-ttu-id="09747-150">Hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, и `Remove-AzureRmDnsZone` все командлеты поддерживают запросы подтверждения.</span><span class="sxs-lookup"><span data-stu-id="09747-150">hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="09747-151">Оба `New-AzureRmDnsZone` и `Set-AzureRmDnsZone` запрашивать подтверждение при hello `$ConfirmPreference` PowerShell Привилегированная переменная имеет значение `Medium` или ниже.</span><span class="sxs-lookup"><span data-stu-id="09747-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="09747-152">Из-за toohello потенциально высокая степень влияния на удаления зоны DNS, hello `Remove-AzureRmDnsZone` командлет запрашивает подтверждение, если hello `$ConfirmPreference` переменной PowerShell имеет любое значение, отличное от `None`.</span><span class="sxs-lookup"><span data-stu-id="09747-152">Due toohello potentially high impact of deleting a DNS zone, hello `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="09747-153">Так как значение по умолчанию hello `$ConfirmPreference` — `High`только `Remove-AzureRmDnsZone` запрашивает подтверждение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="09747-153">Since hello default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="09747-154">Можно переопределить текущего hello `$ConfirmPreference` параметр с помощью hello `-Confirm` параметра.</span><span class="sxs-lookup"><span data-stu-id="09747-154">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="09747-155">При указании `-Confirm` или `-Confirm:$True` , hello командлет запросит подтверждение перед его запуска.</span><span class="sxs-lookup"><span data-stu-id="09747-155">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="09747-156">При указании `-Confirm:$False` , командлет hello не запрашивает вашего подтверждения.</span><span class="sxs-lookup"><span data-stu-id="09747-156">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="09747-157">Дополнительные сведения об элементах `-Confirm` и `$ConfirmPreference` см. в статье о [привилегированных переменных](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="09747-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09747-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09747-158">Next steps</span></span>

<span data-ttu-id="09747-159">Узнайте, каким образом слишком[управления наборов записей и записи](dns-operations-recordsets.md) в зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="09747-159">Learn how too[manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="09747-160">Узнайте, каким образом слишком[делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="09747-160">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="09747-161">Просмотрите hello [справочная документация по Azure DNS PowerShell](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="09747-161">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

