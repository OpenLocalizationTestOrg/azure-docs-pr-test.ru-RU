---
title: "Управление записями DNS в службе DNS Azure с помощью Azure PowerShell | Документация Майкрософт"
description: "Управляйте наборами записей и записями DNS в службе Azure DNS при размещении вашего домена в Azure DNS. Все команды PowerShell для операций с наборами записей и записями."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 2962e30e5d9c60b8e786e2ba79647cabfc5925cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="1be60-104">Управление записями и наборами записей DNS в службе DNS Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1be60-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1be60-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="1be60-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="1be60-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1be60-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="1be60-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1be60-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="1be60-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1be60-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="1be60-109">В этой статье описывается, как управлять записями DNS для зоны DNS с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1be60-109">This article shows you how to manage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="1be60-110">Записями DNS также можно управлять с помощью кроссплатформенного [интерфейса командной строки Azure](dns-operations-recordsets-cli.md) или [портала Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1be60-110">DNS records can also be managed by using the cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="1be60-111">Для работы с руководством необходимо [установить Azure PowerShell, войти в учетную запись и создать зону DNS](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="1be60-111">The examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="1be60-112">Введение</span><span class="sxs-lookup"><span data-stu-id="1be60-112">Introduction</span></span>

<span data-ttu-id="1be60-113">Чтобы создавать записи DNS в Azure DNS, нужно понимать, как Azure DNS организует записи DNS в соответствующие наборы записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-113">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="1be60-114">Дополнительные сведения о записях DNS в Azure DNS см. в статье [Зоны и записи DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="1be60-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="1be60-115">Создание записи DNS</span><span class="sxs-lookup"><span data-stu-id="1be60-115">Create a new DNS record</span></span>

<span data-ttu-id="1be60-116">Если вы создаете запись с такими же именем и типом, как у существующей записи, эту новую запись нужно [добавить в существующий набор записей](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="1be60-116">If your new record has the same name and type as an existing record, you need to [add it to the existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="1be60-117">Если имя и тип новой и существующих записей отличаются, вам нужно создать другой набор записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-117">If your new record has a different name and type to all existing records, you need to create a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="1be60-118">Создание записей А в новом наборе записей</span><span class="sxs-lookup"><span data-stu-id="1be60-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="1be60-119">Для создания наборов записей используется командлет `New-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="1be60-119">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="1be60-120">Создавая набор записей, вам нужно определить для него имя, зону, срок жизни (TTL), тип записей и сами создаваемые записи.</span><span class="sxs-lookup"><span data-stu-id="1be60-120">When creating a record set, you need to specify the record set name, the zone, the time to live (TTL), the record type, and the records to be created.</span></span>

<span data-ttu-id="1be60-121">Параметры для добавления записей в набор записей зависят от типа набора записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-121">The parameters for adding records to a record set vary depending on the type of the record set.</span></span> <span data-ttu-id="1be60-122">Например, при использовании набора записей типа A вам нужно указать IP-адрес с использованием параметра `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="1be60-122">For example, when using a record set of type 'A', you need to specify the IP address using the parameter `-IPv4Address`.</span></span> <span data-ttu-id="1be60-123">Другие параметры используются для других типов записей</span><span class="sxs-lookup"><span data-stu-id="1be60-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="1be60-124">(см. [примеры других типов записей](#additional-record-type-examples)).</span><span class="sxs-lookup"><span data-stu-id="1be60-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="1be60-125">В следующем примере создается набор записей с относительным именем www в зоне DNS contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1be60-125">The following example creates a record set with the relative name 'www' in the DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="1be60-126">Полное доменное имя набора записей — www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1be60-126">The fully-qualified name of the record set is 'www.contoso.com'.</span></span> <span data-ttu-id="1be60-127">Тип записи — A, а срок жизни — 3600 секунд.</span><span class="sxs-lookup"><span data-stu-id="1be60-127">The record type is 'A', and the TTL is 3600 seconds.</span></span> <span data-ttu-id="1be60-128">Каждый такой набор содержит одну запись с IP-адресом 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="1be60-128">The record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="1be60-129">Чтобы создать набор записей на вершине зоны (в нашем примере — contoso.com), используйте имя записи @ (без кавычек):</span><span class="sxs-lookup"><span data-stu-id="1be60-129">To create a record set at the 'apex' of a zone (in this case, 'contoso.com'), use the record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="1be60-130">Чтобы создать набор записей, содержащий несколько записей, сначала создайте локальный массив и добавьте записи, а затем передайте этот массив в `New-AzureRmDnsRecordSet`:</span><span class="sxs-lookup"><span data-stu-id="1be60-130">If you need to create a record set containing more than one record, first create a local array and add the records, then pass the array to `New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="1be60-131">[Метаданные набора записей](dns-zones-records.md#tags-and-metadata) используются для связывания данных приложения с каждым набором записей в виде пар "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="1be60-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="1be60-132">В следующем примере показано, как создать набор с двумя записями метаданных: dept=finance и environment=production.</span><span class="sxs-lookup"><span data-stu-id="1be60-132">The following example shows how to create a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="1be60-133">В Azure DNS также поддерживаются пустые наборы записей, которые могут использоваться как заполнители для резервирования имен DNS перед созданием записей DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="1be60-134">Пустые наборы записей, отображаются на панели управления Azure DNS и серверах имен Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-134">Empty record sets are visible in the Azure DNS control plane, but do appear on the Azure DNS name servers.</span></span> <span data-ttu-id="1be60-135">В следующем примере создается пустой набор записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-135">The following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="1be60-136">Создание записей других типов</span><span class="sxs-lookup"><span data-stu-id="1be60-136">Create records of other types</span></span>

<span data-ttu-id="1be60-137">Вы уже узнали, как создавать записи типа А. В следующем примере показано, как создавать записи других типов, поддерживаемые в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-137">Having seen in detail how to create 'A' records, the following examples show how to create records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="1be60-138">Мы покажем, как создать набор записей каждого типа, который будет содержать одну запись.</span><span class="sxs-lookup"><span data-stu-id="1be60-138">In each case, we show how to create a record set containing a single record.</span></span> <span data-ttu-id="1be60-139">Создавать наборы записей других типов (пустые наборы записей или содержащие несколько записей с метаданными) можно на основе представленных выше примеров с записями типа A.</span><span class="sxs-lookup"><span data-stu-id="1be60-139">The earlier examples for 'A' records can be adapted to create record sets of other types containing multiple records, with metadata, or to create empty record sets.</span></span>

<span data-ttu-id="1be60-140">Мы не включаем пример создания набора записей типа SOA, так как такие записи создаются и удаляются только вместе с соответствующей зоной DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-140">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="1be60-141">Тем не менее [записи типа SOA можно изменять, как показано в примере ниже](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="1be60-141">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="1be60-142">Создание набора записей типа AAAA с одной записью</span><span class="sxs-lookup"><span data-stu-id="1be60-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="1be60-143">Создание набора записей типа CNAME с одной записью</span><span class="sxs-lookup"><span data-stu-id="1be60-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="1be60-144">Стандарты DNS не допускают использование записей типа CNAME на вершине зоны (`-Name '@'`), а также использование наборов записей, содержащих более одной записи.</span><span class="sxs-lookup"><span data-stu-id="1be60-144">The DNS standards do not permit CNAME records at the apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="1be60-145">Дополнительные сведения см. в разделе [Записи типа CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="1be60-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="1be60-146">Создание набора записей типа MX с одной записью</span><span class="sxs-lookup"><span data-stu-id="1be60-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="1be60-147">Чтобы создать запись MX на вершине зоны (в данном случае — contoso.com), в этом примере мы используем имя набора записей @.</span><span class="sxs-lookup"><span data-stu-id="1be60-147">In this example, we use the record set name '@' to create an MX record at the zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="1be60-148">Создание набора записей типа NS с одной записью</span><span class="sxs-lookup"><span data-stu-id="1be60-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="1be60-149">Создание набора записей типа PTR с одной записью</span><span class="sxs-lookup"><span data-stu-id="1be60-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="1be60-150">В этом случае my-arpa-zone.com представляет зону обратного просмотра ARPA вашего диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1be60-150">In this case, 'my-arpa-zone.com' represents the ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="1be60-151">Каждая запись PTR в этой зоне соответствует IP-адресу в этом диапазоне.</span><span class="sxs-lookup"><span data-stu-id="1be60-151">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span> <span data-ttu-id="1be60-152">Имя записи 10 — это последний октет IP-адреса в этом диапазоне IP-адресов, представленном данной записью.</span><span class="sxs-lookup"><span data-stu-id="1be60-152">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="1be60-153">Создание набора записей типа SRV с одной записью</span><span class="sxs-lookup"><span data-stu-id="1be60-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="1be60-154">Создавая [набор записей SRV](dns-zones-records.md#srv-records), укажите в его имени *\_службу* и *\_протокол*.</span><span class="sxs-lookup"><span data-stu-id="1be60-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="1be60-155">Если набор записей SRV создается на вершине зоны, включать @ в имя набора записей не нужно.</span><span class="sxs-lookup"><span data-stu-id="1be60-155">There is no need to include '@' in the record set name when creating an SRV record set at the zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="1be60-156">Создание набора записей типа TXT с одной записью</span><span class="sxs-lookup"><span data-stu-id="1be60-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="1be60-157">В следующем примере показано, как создать запись типа ТХТ.</span><span class="sxs-lookup"><span data-stu-id="1be60-157">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="1be60-158">Дополнительные сведения о максимальной длине строки, поддерживаемой в записях типа TXT, см. в разделе [Записи типа TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="1be60-158">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="1be60-159">Получение набора записей</span><span class="sxs-lookup"><span data-stu-id="1be60-159">Get a record set</span></span>

<span data-ttu-id="1be60-160">Чтобы извлечь существующий набор записей, используйте команду `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="1be60-160">To retrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="1be60-161">Этот командлет возвращает локальный объект, представляющий набор записей в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-161">This cmdlet returns a local object that represents the record set in Azure DNS.</span></span>

<span data-ttu-id="1be60-162">Как и в случае с командлетом `New-AzureRmDnsRecordSet`, имя записи должно быть *относительным*, т. е. оно не должно содержать имя зоны.</span><span class="sxs-lookup"><span data-stu-id="1be60-162">As with `New-AzureRmDnsRecordSet`, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="1be60-163">Также необходимо определить тип записи и зону, содержащую набор записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-163">You also need to specify the record type, and the zone containing the record set.</span></span>

<span data-ttu-id="1be60-164">В следующем примере показано, как получить набор записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-164">The following example shows how to retrieve a record set.</span></span> <span data-ttu-id="1be60-165">В этом примере зона определяется с помощью `-ZoneName` и `-ResourceGroupName` параметров.</span><span class="sxs-lookup"><span data-stu-id="1be60-165">In this example, the zone is specified using the `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="1be60-166">Кроме того, зону можно указать с помощью объекта зоны, переданного с помощью параметра `-Zone`.</span><span class="sxs-lookup"><span data-stu-id="1be60-166">Alternatively, you can also specify the zone using a zone object, passed using the `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="1be60-167">Перечисление наборов записей</span><span class="sxs-lookup"><span data-stu-id="1be60-167">List record sets</span></span>

<span data-ttu-id="1be60-168">Чтобы перечислить наборы записей в зоне, можно также использовать `Get-AzureRmDnsZone`, опустив параметры `-Name` или `-RecordType`.</span><span class="sxs-lookup"><span data-stu-id="1be60-168">You can also use `Get-AzureRmDnsZone` to list record sets in a zone, by omitting the `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="1be60-169">В следующем примере возвращаются все наборы записей в зоне:</span><span class="sxs-lookup"><span data-stu-id="1be60-169">The following example returns all record sets in the zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="1be60-170">В следующем примере показано, как можно получить, все наборы записей нужного типа, указав тип набора записей и опустив его имя:</span><span class="sxs-lookup"><span data-stu-id="1be60-170">The following example shows how all record sets of a given type can be retrieved by specifying the record type while omitting the record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="1be60-171">Чтобы получить все наборы записей разных типов с нужным именем, необходимо получить все наборы записей, а затем отфильтровать результаты:</span><span class="sxs-lookup"><span data-stu-id="1be60-171">To retrieve all record sets with a given name, across record types, you need to retrieve all record sets and then filter the results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="1be60-172">Во всех этих примерах зону можно определить с помощью параметров `-ZoneName` и `-ResourceGroupName` (как и показано) или с помощью объекта зоны:</span><span class="sxs-lookup"><span data-stu-id="1be60-172">In all the above examples, the zone can be specified either by using the `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="1be60-173">Добавление записи в существующий набор записей</span><span class="sxs-lookup"><span data-stu-id="1be60-173">Add a record to an existing record set</span></span>

<span data-ttu-id="1be60-174">Чтобы добавить запись в существующий набор записей, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="1be60-174">To add a record to an existing record set, follow the following three steps:</span></span>

1. <span data-ttu-id="1be60-175">Получите существующий набор записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-175">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="1be60-176">Добавьте новую запись в локальный набор записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-176">Add the new record to the local record set.</span></span> <span data-ttu-id="1be60-177">Эта операция выполняется в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="1be60-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="1be60-178">Зафиксируйте изменения в службе Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-178">Commit the change back to the Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="1be60-179">С помощью `Set-AzureRmDnsRecordSet` существующий набор записей в Azure DNS (и все записи, которые он содержит) *будет заменен* указанным набором записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-179">Using `Set-AzureRmDnsRecordSet` *replaces* the existing record set in Azure DNS (and all records it contains) with the record set specified.</span></span> <span data-ttu-id="1be60-180">[Проверки Etag](dns-zones-records.md#etags) помогают избежать перезаписи параллельных изменений.</span><span class="sxs-lookup"><span data-stu-id="1be60-180">[Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="1be60-181">Чтобы отменить эти проверки, укажите необязательный параметр `-Overwrite`.</span><span class="sxs-lookup"><span data-stu-id="1be60-181">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="1be60-182">Последовательность операций также можно *направить в конвейер*. Это значит, что объект набора записей передается с помощью конвейера, а не как параметр:</span><span class="sxs-lookup"><span data-stu-id="1be60-182">This sequence of operations can also be *piped*, meaning you pass the record set object by using the pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="1be60-183">Приведенные выше примеры иллюстрируют добавление записи типа А в существующий набор записей типа A.</span><span class="sxs-lookup"><span data-stu-id="1be60-183">The examples above show how to add an 'A' record to an existing record set of type 'A'.</span></span> <span data-ttu-id="1be60-184">Аналогичная последовательность операций используется и для добавления записей в наборы записей других типов. Для этого в `Add-AzureRmDnsRecordConfig` нужно просто заменить параметр `-Ipv4Address` параметром, соответствующим нужному типу записи.</span><span class="sxs-lookup"><span data-stu-id="1be60-184">A similar sequence of operations is used to add records to record sets of other types, substituting the `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific to each record type.</span></span> <span data-ttu-id="1be60-185">Как видно в [примерах с другими типами записей](#additional-record-type-examples) (см. выше), используемые для каждого типа записи параметры соответствуют параметрам в командлете `New-AzureRmDnsRecordConfig`.</span><span class="sxs-lookup"><span data-stu-id="1be60-185">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="1be60-186">Наборы записей типа CNAME или SOA не могут содержать более одной записи.</span><span class="sxs-lookup"><span data-stu-id="1be60-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="1be60-187">Это ограничение определяется общими стандартами DNS,</span><span class="sxs-lookup"><span data-stu-id="1be60-187">This constraint arises from the DNS standards.</span></span> <span data-ttu-id="1be60-188">а не Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="1be60-189">Удаление записи из существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="1be60-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="1be60-190">Процедура удаления записи из существующего набора записей аналогична процедуре добавления в такой набор.</span><span class="sxs-lookup"><span data-stu-id="1be60-190">The process to remove a record from a record set is similar to the process to add a record to an existing record set:</span></span>

1. <span data-ttu-id="1be60-191">Получите существующий набор записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-191">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="1be60-192">Удалите запись из объекта локального набора записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-192">Remove the record from the local record set object.</span></span> <span data-ttu-id="1be60-193">Эта операция выполняется в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="1be60-193">This is an off-line operation.</span></span> <span data-ttu-id="1be60-194">Удаляемая запись должна точно соответствовать существующей записи по всем параметрам.</span><span class="sxs-lookup"><span data-stu-id="1be60-194">The record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="1be60-195">Зафиксируйте изменения в службе Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-195">Commit the change back to the Azure DNS service.</span></span> <span data-ttu-id="1be60-196">Чтобы отменить [проверки Etag](dns-zones-records.md#etags) (проверки перезаписи параллельных изменений), используйте необязательный параметр `-Overwrite`.</span><span class="sxs-lookup"><span data-stu-id="1be60-196">Use the optional `-Overwrite` switch to suppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="1be60-197">Используя приведенную выше последовательность для удаления последней записи из набора, вы не удалите набор, а оставите его пустым.</span><span class="sxs-lookup"><span data-stu-id="1be60-197">Using the above sequence to remove the last record from a record set does not delete the record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="1be60-198">Как удалить сам набор записей, описано в разделе [Удаление набора записей](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="1be60-198">To remove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="1be60-199">Как и при добавлении записей в набор записей, последовательность операций для удаления набора записей также можно объединить в конвейер:</span><span class="sxs-lookup"><span data-stu-id="1be60-199">Similarly to adding records to a record set, the sequence of operations to remove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="1be60-200">Поддержку разных типов записей можно реализовать, передав в `Remove-AzureRmDnsRecordSet` соответствующие каждому типу параметры.</span><span class="sxs-lookup"><span data-stu-id="1be60-200">Different record types are supported by passing the appropriate type-specific parameters to `Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="1be60-201">Как видно в [примерах с другими типами записей](#additional-record-type-examples) (см. выше), используемые для каждого типа записи параметры соответствуют параметрам в командлете `New-AzureRmDnsRecordConfig`.</span><span class="sxs-lookup"><span data-stu-id="1be60-201">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="1be60-202">Обновление существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="1be60-202">Modify an existing record set</span></span>

<span data-ttu-id="1be60-203">Процедура изменения существующего набора записей аналогична процедуре добавления записей в набор записей и их удаления оттуда.</span><span class="sxs-lookup"><span data-stu-id="1be60-203">The steps for modifying an existing record set are similar to the steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="1be60-204">Извлеките существующий набор записей, используя командлет `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="1be60-204">Retrieve the existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="1be60-205">Чтобы изменить локальный объект набора записей, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1be60-205">Modify the local record set object by:</span></span>
    * <span data-ttu-id="1be60-206">добавьте или удалите записи;</span><span class="sxs-lookup"><span data-stu-id="1be60-206">Adding or removing records</span></span>
    * <span data-ttu-id="1be60-207">измените параметры существующих записей;</span><span class="sxs-lookup"><span data-stu-id="1be60-207">Changing the parameters of existing records</span></span>
    * <span data-ttu-id="1be60-208">измените метаданные и время жизни (TTL) для набора записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-208">Changing the record set metadata and time to live (TTL)</span></span>
3. <span data-ttu-id="1be60-209">Зафиксируйте изменения с помощью командлета `Set-AzureRmDnsRecordSet` .</span><span class="sxs-lookup"><span data-stu-id="1be60-209">Commit your changes by using the `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="1be60-210">Существующий набор записей в Azure DNS *будет заменен* указанным набором.</span><span class="sxs-lookup"><span data-stu-id="1be60-210">This *replaces* the existing record set in Azure DNS with the record set specified.</span></span>

<span data-ttu-id="1be60-211">При использовании `Set-AzureRmDnsRecordSet` избежать перезаписи параллельных изменений помогут [проверки Etag](dns-zones-records.md#etags).</span><span class="sxs-lookup"><span data-stu-id="1be60-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="1be60-212">Чтобы отменить эти проверки, укажите необязательный параметр `-Overwrite`.</span><span class="sxs-lookup"><span data-stu-id="1be60-212">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

### <a name="to-update-a-record-in-an-existing-record-set"></a><span data-ttu-id="1be60-213">Обновление записи в существующем наборе записей</span><span class="sxs-lookup"><span data-stu-id="1be60-213">To update a record in an existing record set</span></span>

<span data-ttu-id="1be60-214">В данном примере мы изменим IP-адрес существующей записи типа A:</span><span class="sxs-lookup"><span data-stu-id="1be60-214">In this example, we change the IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="1be60-215">Изменение записи типа SOA</span><span class="sxs-lookup"><span data-stu-id="1be60-215">To modify an SOA record</span></span>

<span data-ttu-id="1be60-216">В автоматически созданном наборе записей типа SOA на вершине зоны (`-Name "@"`, включая кавычки) добавлять или удалять записи нельзя.</span><span class="sxs-lookup"><span data-stu-id="1be60-216">You cannot add or remove records from the automatically created SOA record set at the zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="1be60-217">Однако вы можете изменить любые параметры в записи типа SOA (за исключением параметра "Узел") и TTL набора записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-217">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

<span data-ttu-id="1be60-218">В следующем примере показано, как изменить свойство *Email* записи типа SOA:</span><span class="sxs-lookup"><span data-stu-id="1be60-218">The following example shows how to change the *Email* property of the SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="1be60-219">Изменение записи NS на вершине зоны</span><span class="sxs-lookup"><span data-stu-id="1be60-219">To modify NS records at the zone apex</span></span>

<span data-ttu-id="1be60-220">Набор записей типа NS на вершине зоны автоматически создается вместе с каждой зоной DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-220">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="1be60-221">Он содержит имена DNS-серверов Azure, назначенные зоне.</span><span class="sxs-lookup"><span data-stu-id="1be60-221">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="1be60-222">Вы можете добавить дополнительные имена серверов в этот набор записей NS, обеспечив поддержку совместного размещения доменов с использованием более чем одного поставщика DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-222">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="1be60-223">Вы также можете изменить срок жизни и метаданные для этого набора записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-223">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="1be60-224">При этом вы не можете удалить или изменить предварительно заполненные серверы доменных имен Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-224">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="1be60-225">Обратите внимание, что это относится только к набору записей NS на вершине зоны.</span><span class="sxs-lookup"><span data-stu-id="1be60-225">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="1be60-226">Другие наборы записей NS в зоне (используемые для делегирования дочерних зон) можно изменять без ограничений.</span><span class="sxs-lookup"><span data-stu-id="1be60-226">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="1be60-227">В следующем примере показано, как добавить дополнительный сервер в набор записей NS на вершине зоны:</span><span class="sxs-lookup"><span data-stu-id="1be60-227">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-record-set-metadata"></a><span data-ttu-id="1be60-228">Изменение метаданных набора записей</span><span class="sxs-lookup"><span data-stu-id="1be60-228">To modify record set metadata</span></span>

<span data-ttu-id="1be60-229">[Метаданные набора записей](dns-zones-records.md#tags-and-metadata) используются для связывания данных приложения с каждым набором записей в виде пар "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="1be60-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="1be60-230">В примере ниже показано, как изменить метаданные существующего набора записей:</span><span class="sxs-lookup"><span data-stu-id="1be60-230">The following example shows how to modify the metadata of an existing record set:</span></span>

```powershell
# Get the record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="1be60-231">Удаление набора записей</span><span class="sxs-lookup"><span data-stu-id="1be60-231">Delete a record set</span></span>

<span data-ttu-id="1be60-232">Наборы записей можно удалять с помощью командлета `Remove-AzureRmDnsRecordSet` .</span><span class="sxs-lookup"><span data-stu-id="1be60-232">Record sets can be deleted by using the `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="1be60-233">При удалении набора записей также удаляются все содержащиеся в нем записи.</span><span class="sxs-lookup"><span data-stu-id="1be60-233">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="1be60-234">Удалить наборы записей типа SOA и NS на вершине зоны (`-Name '@'`) нельзя.</span><span class="sxs-lookup"><span data-stu-id="1be60-234">You cannot delete the SOA and NS record sets at the zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="1be60-235">Эти записи создаются и удаляются в Azure DNS автоматически вместе с зоной.</span><span class="sxs-lookup"><span data-stu-id="1be60-235">Azure DNS created these automatically when the zone was created, and deletes them automatically when the zone is deleted.</span></span>

<span data-ttu-id="1be60-236">В примере ниже показано, как удалить набор записей.</span><span class="sxs-lookup"><span data-stu-id="1be60-236">The following example shows how to delete a record set.</span></span> <span data-ttu-id="1be60-237">В этом примере имя и тип набора записей, имя зоны и группа ресурсов указываются явным образом.</span><span class="sxs-lookup"><span data-stu-id="1be60-237">In this example, the record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="1be60-238">Также набор записей можно указать по имени, типу и зоне (определяется с помощью объекта):</span><span class="sxs-lookup"><span data-stu-id="1be60-238">Alternatively, the record set can be specified by name and type, and the zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="1be60-239">Либо же можно указать сам набор записей, используя объект набора записей:</span><span class="sxs-lookup"><span data-stu-id="1be60-239">As a third option, the record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="1be60-240">Указывая набор удаляемых записей с помощью объекта, вы можете выполнить [проверки Etag](dns-zones-records.md#etags), чтобы избежать удаления параллельных изменений.</span><span class="sxs-lookup"><span data-stu-id="1be60-240">When you specify the record set to be deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="1be60-241">Чтобы отменить эти проверки, укажите необязательный параметр `-Overwrite`.</span><span class="sxs-lookup"><span data-stu-id="1be60-241">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="1be60-242">Объект набора записей также можно направить в конвейер, а не передать в качестве параметра:</span><span class="sxs-lookup"><span data-stu-id="1be60-242">The record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="1be60-243">Запросы на подтверждение</span><span class="sxs-lookup"><span data-stu-id="1be60-243">Confirmation prompts</span></span>

<span data-ttu-id="1be60-244">Командлеты `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet` и `Remove-AzureRmDnsRecordSet` поддерживают запросы на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="1be60-244">The `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="1be60-245">Каждый командлет запрашивает подтверждение, если привилегированная переменная `$ConfirmPreference` в PowerShell имеет значение `Medium` или ниже.</span><span class="sxs-lookup"><span data-stu-id="1be60-245">Each cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="1be60-246">Так как по умолчанию переменной `$ConfirmPreference` присвоено значение `High`, эти запросы не используются при использовании стандартных параметров PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1be60-246">Since the default value for `$ConfirmPreference` is `High`, these prompts are not given when using the default PowerShell settings.</span></span>

<span data-ttu-id="1be60-247">Текущее значение `$ConfirmPreference` можно переопределить с помощью параметра `-Confirm`.</span><span class="sxs-lookup"><span data-stu-id="1be60-247">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="1be60-248">Если вы определите `-Confirm` или `-Confirm:$True`, командлет будет запрашивать подтверждение перед выполнением.</span><span class="sxs-lookup"><span data-stu-id="1be60-248">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="1be60-249">Если вы определите `-Confirm:$False`, командлет не будет запрашивать подтверждение.</span><span class="sxs-lookup"><span data-stu-id="1be60-249">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="1be60-250">Дополнительные сведения об элементах `-Confirm` и `$ConfirmPreference` см. в статье о [привилегированных переменных](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="1be60-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1be60-251">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1be60-251">Next steps</span></span>

<span data-ttu-id="1be60-252">См. дополнительные сведения о [зонах и записях в Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="1be60-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="1be60-253">Узнайте, как [защитить зоны и записи](dns-protect-zones-recordsets.md) при использовании Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1be60-253">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="1be60-254">Просмотрите [справочную документацию по Azure DNS PowerShell](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="1be60-254">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
