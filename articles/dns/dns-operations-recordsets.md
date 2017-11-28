---
title: "Записывает aaaManage DNS в Azure DNS, с помощью Azure PowerShell | Документы Microsoft"
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
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="c498d-104">Управление записями и наборами записей DNS в службе DNS Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c498d-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c498d-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c498d-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="c498d-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c498d-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="c498d-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c498d-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="c498d-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c498d-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="c498d-109">В этой статье показано, как записывает toomanage DNS для зоны DNS с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c498d-109">This article shows you how toomanage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="c498d-110">DNS-записи можно также управлять с помощью hello кросс платформенных [Azure CLI](dns-operations-recordsets-cli.md) или hello [портал Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c498d-110">DNS records can also be managed by using hello cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="c498d-111">Hello в этой статье примерах уже имеется [Azure PowerShell, вход и создали зоны DNS](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="c498d-111">hello examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="c498d-112">Введение</span><span class="sxs-lookup"><span data-stu-id="c498d-112">Introduction</span></span>

<span data-ttu-id="c498d-113">Прежде чем создавать DNS-записи в Azure DNS, необходимо сначала toounderstand как Azure DNS организует DNS-записей в наборы записей DNS.</span><span class="sxs-lookup"><span data-stu-id="c498d-113">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="c498d-114">Дополнительные сведения о записях DNS в Azure DNS см. в статье [Зоны и записи DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="c498d-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="c498d-115">Создание записи DNS</span><span class="sxs-lookup"><span data-stu-id="c498d-115">Create a new DNS record</span></span>

<span data-ttu-id="c498d-116">Если новую запись имеет hello совпадают имя и тип в качестве существующей записи, необходимо слишком[добавьте его в существующий набор записей toohello](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="c498d-116">If your new record has hello same name and type as an existing record, you need too[add it toohello existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="c498d-117">Если новую запись имеет разные имена и типы tooall существующие записи, то необходимо toocreate нового набора записей.</span><span class="sxs-lookup"><span data-stu-id="c498d-117">If your new record has a different name and type tooall existing records, you need toocreate a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="c498d-118">Создание записей А в новом наборе записей</span><span class="sxs-lookup"><span data-stu-id="c498d-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="c498d-119">Создание наборов записей с помощью hello `New-AzureRmDnsRecordSet` командлета.</span><span class="sxs-lookup"><span data-stu-id="c498d-119">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="c498d-120">При создании набора записей, необходимо имя набора записей toospecify hello, hello зоны, hello время toolive (TTL), тип записи hello и toobe записей hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-120">When creating a record set, you need toospecify hello record set name, hello zone, hello time toolive (TTL), hello record type, and hello records toobe created.</span></span>

<span data-ttu-id="c498d-121">Hello параметры для добавления набора записей tooa записей зависит от типа hello hello набор записей.</span><span class="sxs-lookup"><span data-stu-id="c498d-121">hello parameters for adding records tooa record set vary depending on hello type of hello record set.</span></span> <span data-ttu-id="c498d-122">Например, при использовании набора записей типа «A», требуется toospecify hello IP-адрес с помощью параметра hello `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="c498d-122">For example, when using a record set of type 'A', you need toospecify hello IP address using hello parameter `-IPv4Address`.</span></span> <span data-ttu-id="c498d-123">Другие параметры используются для других типов записей</span><span class="sxs-lookup"><span data-stu-id="c498d-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="c498d-124">(см. [примеры других типов записей](#additional-record-type-examples)).</span><span class="sxs-lookup"><span data-stu-id="c498d-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="c498d-125">Hello пример создает записей с hello относительное имя «www», в зону DNS «contoso.com» hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-125">hello following example creates a record set with hello relative name 'www' in hello DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="c498d-126">Hello полное имя набора записей hello — «www.contoso.com».</span><span class="sxs-lookup"><span data-stu-id="c498d-126">hello fully-qualified name of hello record set is 'www.contoso.com'.</span></span> <span data-ttu-id="c498d-127">Тип записи Hello «A», который hello TTL 3600 секунд.</span><span class="sxs-lookup"><span data-stu-id="c498d-127">hello record type is 'A', and hello TTL is 3600 seconds.</span></span> <span data-ttu-id="c498d-128">набор записей Hello содержит одну запись, с IP-адресом "1.2.3.4».</span><span class="sxs-lookup"><span data-stu-id="c498d-128">hello record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="c498d-129">toocreate набор записей в зоне «вершине» hello (в данном случае «contoso.com»), используйте имя набора записей hello "@" (без кавычек):</span><span class="sxs-lookup"><span data-stu-id="c498d-129">toocreate a record set at hello 'apex' of a zone (in this case, 'contoso.com'), use hello record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="c498d-130">Если вам требуется toocreate набор записей, содержащий несколько записей, сначала создать локальный массив и добавить записи hello, а затем передать массив hello слишком`New-AzureRmDnsRecordSet` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c498d-130">If you need toocreate a record set containing more than one record, first create a local array and add hello records, then pass hello array too`New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="c498d-131">[Набор записей метаданных](dns-zones-records.md#tags-and-metadata) может быть используется tooassociate данных приложения с каждым набором записей, как пары "ключ значение".</span><span class="sxs-lookup"><span data-stu-id="c498d-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="c498d-132">Hello следующем примере показано, как toocreate набор записей с две записи метаданных "dept = процент" и "среды производственного =".</span><span class="sxs-lookup"><span data-stu-id="c498d-132">hello following example shows how toocreate a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="c498d-133">Azure DNS также поддерживает «empty» наборы записей, которые может выступать в качестве tooreserve заполнитель DNS-имя перед созданием записи DNS.</span><span class="sxs-lookup"><span data-stu-id="c498d-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="c498d-134">Пустые наборы записей, отображаются в плоскости управления hello Azure DNS, но отображаться на hello Azure DNS-серверами.</span><span class="sxs-lookup"><span data-stu-id="c498d-134">Empty record sets are visible in hello Azure DNS control plane, but do appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="c498d-135">Следующий пример Hello создает пустой набор записей:</span><span class="sxs-lookup"><span data-stu-id="c498d-135">hello following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="c498d-136">Создание записей других типов</span><span class="sxs-lookup"><span data-stu-id="c498d-136">Create records of other types</span></span>

<span data-ttu-id="c498d-137">Рассматривать подробно порядок записей toocreate «A» hello, в следующих примерах показано, как записи toocreate других записи типы, поддерживаемые системой Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c498d-137">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="c498d-138">В каждом случае показано, как toocreate запись набор, содержащий одну запись.</span><span class="sxs-lookup"><span data-stu-id="c498d-138">In each case, we show how toocreate a record set containing a single record.</span></span> <span data-ttu-id="c498d-139">Hello предыдущих примерах для записей 'A' может быть адаптирован toocreate наборы записей других типов, содержащих несколько записей с метаданными, или пустая запись toocreate задает.</span><span class="sxs-lookup"><span data-stu-id="c498d-139">hello earlier examples for 'A' records can be adapted toocreate record sets of other types containing multiple records, with metadata, or toocreate empty record sets.</span></span>

<span data-ttu-id="c498d-140">Мы не предоставляем toocreate примере SOA набор записей, так как создаются SOA и удалены вместе с каждой зоны DNS и не удается создать или удалить отдельно.</span><span class="sxs-lookup"><span data-stu-id="c498d-140">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="c498d-141">Тем не менее [SOA могут быть изменены, как показано в пример hello](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="c498d-141">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="c498d-142">Создание набора записей типа AAAA с одной записью</span><span class="sxs-lookup"><span data-stu-id="c498d-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="c498d-143">Создание набора записей типа CNAME с одной записью</span><span class="sxs-lookup"><span data-stu-id="c498d-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="c498d-144">Hello стандартах DNS не допускают записи CNAME на вершине hello зоны (`-Name '@'`), и не следует разрешать или запрещать наборы записей, содержащая более одной записи.</span><span class="sxs-lookup"><span data-stu-id="c498d-144">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="c498d-145">Дополнительные сведения см. в разделе [Записи типа CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="c498d-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="c498d-146">Создание набора записей типа MX с одной записью</span><span class="sxs-lookup"><span data-stu-id="c498d-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="c498d-147">В этом примере мы используем имя набора записей hello ' @' toocreate MX-записи на вершине зоны hello (в данном случае «contoso.com»).</span><span class="sxs-lookup"><span data-stu-id="c498d-147">In this example, we use hello record set name '@' toocreate an MX record at hello zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="c498d-148">Создание набора записей типа NS с одной записью</span><span class="sxs-lookup"><span data-stu-id="c498d-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="c498d-149">Создание набора записей типа PTR с одной записью</span><span class="sxs-lookup"><span data-stu-id="c498d-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="c498d-150">В этом случае "my-arpa-zone.com" представляет hello ARPA зоны обратного просмотра, представляющий ваш диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c498d-150">In this case, 'my-arpa-zone.com' represents hello ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="c498d-151">Каждая запись PTR в этой зоне соответствует tooan IP-адрес в этот диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c498d-151">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span> <span data-ttu-id="c498d-152">Имя записи Hello "10" представляет hello последний октет hello IP-адрес в этот диапазон IP-адресов, представленного данной записью.</span><span class="sxs-lookup"><span data-stu-id="c498d-152">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="c498d-153">Создание набора записей типа SRV с одной записью</span><span class="sxs-lookup"><span data-stu-id="c498d-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="c498d-154">При создании [набор записей типа SRV](dns-zones-records.md#srv-records), укажите hello  *\_службы* и  *\_протокола* в hello имя набора записей.</span><span class="sxs-lookup"><span data-stu-id="c498d-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="c498d-155">Нет нет необходимости tooinclude "@" в hello запись имя набора при создании записи SRV набора в вершине зоны hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-155">There is no need tooinclude '@' in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="c498d-156">Создание набора записей типа TXT с одной записью</span><span class="sxs-lookup"><span data-stu-id="c498d-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="c498d-157">Hello следующем примере показано, как записать toocreate TXT.</span><span class="sxs-lookup"><span data-stu-id="c498d-157">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="c498d-158">Дополнительные сведения о hello Максимальная длина строки поддерживается в записи TXT в разделе [записи TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="c498d-158">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="c498d-159">Получение набора записей</span><span class="sxs-lookup"><span data-stu-id="c498d-159">Get a record set</span></span>

<span data-ttu-id="c498d-160">использовать существующий набор записей, tooretrieve `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="c498d-160">tooretrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="c498d-161">Этот командлет возвращает локальный объект, представляющий hello записи в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c498d-161">This cmdlet returns a local object that represents hello record set in Azure DNS.</span></span>

<span data-ttu-id="c498d-162">Как и в `New-AzureRmDnsRecordSet`, должно быть имя набора записей hello *относительный* имя, то есть его необходимо исключить hello имя зоны.</span><span class="sxs-lookup"><span data-stu-id="c498d-162">As with `New-AzureRmDnsRecordSet`, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="c498d-163">Необходимо также тип записи toospecify hello и hello зону, содержащую набор записей hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-163">You also need toospecify hello record type, and hello zone containing hello record set.</span></span>

<span data-ttu-id="c498d-164">Hello примере показан способ tooretrieve набор записей.</span><span class="sxs-lookup"><span data-stu-id="c498d-164">hello following example shows how tooretrieve a record set.</span></span> <span data-ttu-id="c498d-165">В этом примере hello зоны задается с помощью hello `-ZoneName` и `-ResourceGroupName` параметров.</span><span class="sxs-lookup"><span data-stu-id="c498d-165">In this example, hello zone is specified using hello `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="c498d-166">Кроме того, можно также указать hello зоны с помощью объекта зоны, переданные с помощью hello `-Zone` параметра.</span><span class="sxs-lookup"><span data-stu-id="c498d-166">Alternatively, you can also specify hello zone using a zone object, passed using hello `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="c498d-167">Перечисление наборов записей</span><span class="sxs-lookup"><span data-stu-id="c498d-167">List record sets</span></span>

<span data-ttu-id="c498d-168">Можно также использовать `Get-AzureRmDnsZone` наборов toolist записей в зоне, пропустив hello `-Name` и/или `-RecordType` параметров.</span><span class="sxs-lookup"><span data-stu-id="c498d-168">You can also use `Get-AzureRmDnsZone` toolist record sets in a zone, by omitting hello `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="c498d-169">Hello следующий пример возвращает все записи задает в зоне hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-169">hello following example returns all record sets in hello zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="c498d-170">Hello следующем примере показано, как все записи наборов данного типа, можно получить, указав тип записи hello, пока пропуск записи hello имя набора:</span><span class="sxs-lookup"><span data-stu-id="c498d-170">hello following example shows how all record sets of a given type can be retrieved by specifying hello record type while omitting hello record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="c498d-171">Задает все записи с заданным именем, tooretrieve разных типов записей, необходимо tooretrieve все наборы записей, а затем результаты hello фильтра:</span><span class="sxs-lookup"><span data-stu-id="c498d-171">tooretrieve all record sets with a given name, across record types, you need tooretrieve all record sets and then filter hello results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="c498d-172">В все hello выше примеры hello зоны может быть указан с помощью hello `-ZoneName` и `-ResourceGroupName`параметров (как показано), или путем указания объекта зоны:</span><span class="sxs-lookup"><span data-stu-id="c498d-172">In all hello above examples, hello zone can be specified either by using hello `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="c498d-173">Добавление записей tooan существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="c498d-173">Add a record tooan existing record set</span></span>

<span data-ttu-id="c498d-174">tooadd существующей записи записей tooan задать, выполните следующие три шага hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-174">tooadd a record tooan existing record set, follow hello following three steps:</span></span>

1. <span data-ttu-id="c498d-175">Получение существующего набора записей hello</span><span class="sxs-lookup"><span data-stu-id="c498d-175">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="c498d-176">Добавьте hello новых записей toohello локальный набор записей.</span><span class="sxs-lookup"><span data-stu-id="c498d-176">Add hello new record toohello local record set.</span></span> <span data-ttu-id="c498d-177">Эта операция выполняется в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="c498d-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="c498d-178">Зафиксируйте hello изменений назад toohello служба Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c498d-178">Commit hello change back toohello Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="c498d-179">С помощью `Set-AzureRmDnsRecordSet` *заменяет* hello существующих записей в Azure DNS (и все записи, он содержит) с указанного набора записей hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-179">Using `Set-AzureRmDnsRecordSet` *replaces* hello existing record set in Azure DNS (and all records it contains) with hello record set specified.</span></span> <span data-ttu-id="c498d-180">[Проверяет eTag](dns-zones-records.md#etags) используются tooensure параллельных изменений не перезаписываются.</span><span class="sxs-lookup"><span data-stu-id="c498d-180">[Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="c498d-181">Можно использовать необязательный hello `-Overwrite` переключения toosuppress этих проверок.</span><span class="sxs-lookup"><span data-stu-id="c498d-181">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="c498d-182">Эта последовательность операций также может быть *по конвейеру*, то есть передать hello объекта набора записей, через канал hello вместо передачи его в качестве параметра:</span><span class="sxs-lookup"><span data-stu-id="c498d-182">This sequence of operations can also be *piped*, meaning you pass hello record set object by using hello pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="c498d-183">Hello примеры выше показывают, как задать tooadd 'A' записей tooan существующей записи типа «A».</span><span class="sxs-lookup"><span data-stu-id="c498d-183">hello examples above show how tooadd an 'A' record tooan existing record set of type 'A'.</span></span> <span data-ttu-id="c498d-184">Аналогичные последовательности операций является наборов toorecord записей используется tooadd других типов, заменив hello `-Ipv4Address` параметр `Add-AzureRmDnsRecordConfig` с другим типом записи tooeach определенные параметры.</span><span class="sxs-lookup"><span data-stu-id="c498d-184">A similar sequence of operations is used tooadd records toorecord sets of other types, substituting hello `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific tooeach record type.</span></span> <span data-ttu-id="c498d-185">Hello параметров для каждого типа записи являются hello же, как и для hello `New-AzureRmDnsRecordConfig` командлет, как показано в [примеры дополнительных тип записи](#additional-record-type-examples) выше.</span><span class="sxs-lookup"><span data-stu-id="c498d-185">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="c498d-186">Наборы записей типа CNAME или SOA не могут содержать более одной записи.</span><span class="sxs-lookup"><span data-stu-id="c498d-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="c498d-187">Это ограничение возникают из-за стандартах DNS hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-187">This constraint arises from hello DNS standards.</span></span> <span data-ttu-id="c498d-188">а не Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c498d-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="c498d-189">Удаление записи из существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="c498d-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="c498d-190">Hello tooremove процесс записи из набора записей — примерно toohello процесс, tooadd в существующие записи tooan записи набора:</span><span class="sxs-lookup"><span data-stu-id="c498d-190">hello process tooremove a record from a record set is similar toohello process tooadd a record tooan existing record set:</span></span>

1. <span data-ttu-id="c498d-191">Получение существующего набора записей hello</span><span class="sxs-lookup"><span data-stu-id="c498d-191">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="c498d-192">Удалите запись hello из hello объекта локальный набор записей.</span><span class="sxs-lookup"><span data-stu-id="c498d-192">Remove hello record from hello local record set object.</span></span> <span data-ttu-id="c498d-193">Эта операция выполняется в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="c498d-193">This is an off-line operation.</span></span> <span data-ttu-id="c498d-194">запись Hello, которое удаляется должно быть в точности совпадать с уже имеющейся записи для всех параметров.</span><span class="sxs-lookup"><span data-stu-id="c498d-194">hello record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="c498d-195">Зафиксируйте hello изменений назад toohello служба Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c498d-195">Commit hello change back toohello Azure DNS service.</span></span> <span data-ttu-id="c498d-196">Используйте hello необязательно `-Overwrite` переключения toosuppress [проверяет Etag](dns-zones-records.md#etags) для параллельных изменений.</span><span class="sxs-lookup"><span data-stu-id="c498d-196">Use hello optional `-Overwrite` switch toosuppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="c498d-197">Hello выше последовательности tooremove hello последней записи из набора записей с помощью удаляет hello: набор записей, а остается пустой набор записей.</span><span class="sxs-lookup"><span data-stu-id="c498d-197">Using hello above sequence tooremove hello last record from a record set does not delete hello record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="c498d-198">см. набор записей, полностью tooremove [удалить набор записей](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="c498d-198">tooremove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="c498d-199">Аналогичным образом набора записи tooa tooadding записей последовательность hello tooremove операций, который также может быть выведен набор записей:</span><span class="sxs-lookup"><span data-stu-id="c498d-199">Similarly tooadding records tooa record set, hello sequence of operations tooremove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="c498d-200">Записей различных типов поддерживаются, передавая соответствующие параметры конкретного типа hello слишком`Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="c498d-200">Different record types are supported by passing hello appropriate type-specific parameters too`Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="c498d-201">Hello параметров для каждого типа записи являются hello же, как и для hello `New-AzureRmDnsRecordConfig` командлет, как показано в [примеры дополнительных тип записи](#additional-record-type-examples) выше.</span><span class="sxs-lookup"><span data-stu-id="c498d-201">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="c498d-202">Обновление существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="c498d-202">Modify an existing record set</span></span>

<span data-ttu-id="c498d-203">Hello действия по изменению существующего набора записей приведены действия, аналогичные toohello предпринять при добавлении или удалении записей из набора записей.</span><span class="sxs-lookup"><span data-stu-id="c498d-203">hello steps for modifying an existing record set are similar toohello steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="c498d-204">Получить задание с помощью существующей записи hello `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="c498d-204">Retrieve hello existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="c498d-205">Измените hello объекта локальный набор записей:</span><span class="sxs-lookup"><span data-stu-id="c498d-205">Modify hello local record set object by:</span></span>
    * <span data-ttu-id="c498d-206">добавьте или удалите записи;</span><span class="sxs-lookup"><span data-stu-id="c498d-206">Adding or removing records</span></span>
    * <span data-ttu-id="c498d-207">Изменение параметров hello существующих записей</span><span class="sxs-lookup"><span data-stu-id="c498d-207">Changing hello parameters of existing records</span></span>
    * <span data-ttu-id="c498d-208">Изменение записи hello набора метаданных и времени toolive (TTL)</span><span class="sxs-lookup"><span data-stu-id="c498d-208">Changing hello record set metadata and time toolive (TTL)</span></span>
3. <span data-ttu-id="c498d-209">Фиксация изменений с помощью hello `Set-AzureRmDnsRecordSet` командлета.</span><span class="sxs-lookup"><span data-stu-id="c498d-209">Commit your changes by using hello `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="c498d-210">Это *заменяет* hello существующих записей в Azure DNS с указанного набора записей hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-210">This *replaces* hello existing record set in Azure DNS with hello record set specified.</span></span>

<span data-ttu-id="c498d-211">При использовании `Set-AzureRmDnsRecordSet`, [проверяет Etag](dns-zones-records.md#etags) используются tooensure параллельных изменений не перезаписываются.</span><span class="sxs-lookup"><span data-stu-id="c498d-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="c498d-212">Можно использовать необязательный hello `-Overwrite` переключения toosuppress этих проверок.</span><span class="sxs-lookup"><span data-stu-id="c498d-212">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

### <a name="tooupdate-a-record-in-an-existing-record-set"></a><span data-ttu-id="c498d-213">задать tooupdate записи в существующей записи</span><span class="sxs-lookup"><span data-stu-id="c498d-213">tooupdate a record in an existing record set</span></span>

<span data-ttu-id="c498d-214">В этом примере мы изменяем hello IP-адрес существующего «запись»:</span><span class="sxs-lookup"><span data-stu-id="c498d-214">In this example, we change hello IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="c498d-215">toomodify записи SOA</span><span class="sxs-lookup"><span data-stu-id="c498d-215">toomodify an SOA record</span></span>

<span data-ttu-id="c498d-216">Не удается добавить или удаления записей из hello автоматически создается на вершине зоны hello начальной записи (`-Name "@"`, включая кавычки).</span><span class="sxs-lookup"><span data-stu-id="c498d-216">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="c498d-217">Однако вы можете изменить любые параметры hello в рамках hello начальной записи зоны (кроме «узел») и записи hello задать значение срока ЖИЗНИ.</span><span class="sxs-lookup"><span data-stu-id="c498d-217">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

<span data-ttu-id="c498d-218">Следующий пример показывает как Hello toochange hello *электронной почты* свойство hello начальной записи зоны:</span><span class="sxs-lookup"><span data-stu-id="c498d-218">hello following example shows how toochange hello *Email* property of hello SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="c498d-219">записей toomodify NS на вершине зоны hello</span><span class="sxs-lookup"><span data-stu-id="c498d-219">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="c498d-220">запись NS Hello на вершине зоны hello создается автоматически с каждой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="c498d-220">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="c498d-221">Она содержит имена hello hello Azure имя серверов назначенного toohello зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="c498d-221">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="c498d-222">Можно добавить дополнительное имя серверов toothis NS: набор записей, toosupport совместное размещение домены с более чем одного поставщика DNS.</span><span class="sxs-lookup"><span data-stu-id="c498d-222">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="c498d-223">Можно также изменить hello TTL и метаданные для этого набора записей.</span><span class="sxs-lookup"><span data-stu-id="c498d-223">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="c498d-224">Тем не менее нельзя удалять или изменять hello предварительно заполненных Azure DNS-серверами.</span><span class="sxs-lookup"><span data-stu-id="c498d-224">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="c498d-225">Обратите внимание, что это применимо только toohello NS набора записей на вершине зоны hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-225">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="c498d-226">Другие NS наборов записей в зоне (как в дочерних зонах используется toodelegate) можно изменять без ограничений.</span><span class="sxs-lookup"><span data-stu-id="c498d-226">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="c498d-227">Привет, в следующем примере показано, как tooadd запись NS toohello дополнительное имя сервера задать на вершине зоны hello:</span><span class="sxs-lookup"><span data-stu-id="c498d-227">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a><span data-ttu-id="c498d-228">набор записей toomodify метаданных</span><span class="sxs-lookup"><span data-stu-id="c498d-228">toomodify record set metadata</span></span>

<span data-ttu-id="c498d-229">[Набор записей метаданных](dns-zones-records.md#tags-and-metadata) может быть используется tooassociate данных приложения с каждым набором записей, как пары "ключ значение".</span><span class="sxs-lookup"><span data-stu-id="c498d-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="c498d-230">Hello ниже приведен пример настройки метаданных hello toomodify существующей записи.</span><span class="sxs-lookup"><span data-stu-id="c498d-230">hello following example shows how toomodify hello metadata of an existing record set:</span></span>

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="c498d-231">Удаление набора записей</span><span class="sxs-lookup"><span data-stu-id="c498d-231">Delete a record set</span></span>

<span data-ttu-id="c498d-232">Наборы записей можно удалить с помощью hello `Remove-AzureRmDnsRecordSet` командлета.</span><span class="sxs-lookup"><span data-stu-id="c498d-232">Record sets can be deleted by using hello `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="c498d-233">При удалении набора записей также удаляются все записи в наборе записей hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-233">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="c498d-234">Не удается удалить hello SOA и NS наборов записей в вершине зоны hello (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="c498d-234">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="c498d-235">Azure DNS создается их автоматически при hello зона была создана и удаляет их автоматически при удалении hello зоны.</span><span class="sxs-lookup"><span data-stu-id="c498d-235">Azure DNS created these automatically when hello zone was created, and deletes them automatically when hello zone is deleted.</span></span>

<span data-ttu-id="c498d-236">Hello примере показан способ toodelete набор записей.</span><span class="sxs-lookup"><span data-stu-id="c498d-236">hello following example shows how toodelete a record set.</span></span> <span data-ttu-id="c498d-237">В этом примере имя набора записей hello, набор записей типа, имени зоны и группы ресурсов каждого указаны явным образом.</span><span class="sxs-lookup"><span data-stu-id="c498d-237">In this example, hello record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="c498d-238">Кроме того hello набор записей может быть указан с именем и типом и hello зоны, указанный с помощью объекта:</span><span class="sxs-lookup"><span data-stu-id="c498d-238">Alternatively, hello record set can be specified by name and type, and hello zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="c498d-239">Как третий параметр — набора сам записей hello может быть задано с помощью объекта набора записей:</span><span class="sxs-lookup"><span data-stu-id="c498d-239">As a third option, hello record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="c498d-240">При указании toobe удалена с помощью объекта набора записей, набор записей hello [проверяет Etag](dns-zones-records.md#etags) используются tooensure параллельных изменений не удаляются.</span><span class="sxs-lookup"><span data-stu-id="c498d-240">When you specify hello record set toobe deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="c498d-241">Можно использовать необязательный hello `-Overwrite` переключения toosuppress этих проверок.</span><span class="sxs-lookup"><span data-stu-id="c498d-241">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="c498d-242">Hello объекта набора записей также можно направить вместо передан в качестве параметра:</span><span class="sxs-lookup"><span data-stu-id="c498d-242">hello record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="c498d-243">Запросы на подтверждение</span><span class="sxs-lookup"><span data-stu-id="c498d-243">Confirmation prompts</span></span>

<span data-ttu-id="c498d-244">Hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, и `Remove-AzureRmDnsRecordSet` все командлеты поддерживают запросы подтверждения.</span><span class="sxs-lookup"><span data-stu-id="c498d-244">hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="c498d-245">Каждый командлет запрашивает подтверждение, если hello `$ConfirmPreference` PowerShell Привилегированная переменная имеет значение `Medium` или ниже.</span><span class="sxs-lookup"><span data-stu-id="c498d-245">Each cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="c498d-246">Так как значение по умолчанию hello `$ConfirmPreference` — `High`, не получают эти запросы при использовании параметров PowerShell по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="c498d-246">Since hello default value for `$ConfirmPreference` is `High`, these prompts are not given when using hello default PowerShell settings.</span></span>

<span data-ttu-id="c498d-247">Можно переопределить текущего hello `$ConfirmPreference` параметр с помощью hello `-Confirm` параметра.</span><span class="sxs-lookup"><span data-stu-id="c498d-247">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="c498d-248">При указании `-Confirm` или `-Confirm:$True` , hello командлет запросит подтверждение перед его запуска.</span><span class="sxs-lookup"><span data-stu-id="c498d-248">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="c498d-249">При указании `-Confirm:$False` , командлет hello не запрашивает вашего подтверждения.</span><span class="sxs-lookup"><span data-stu-id="c498d-249">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="c498d-250">Дополнительные сведения об элементах `-Confirm` и `$ConfirmPreference` см. в статье о [привилегированных переменных](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="c498d-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c498d-251">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c498d-251">Next steps</span></span>

<span data-ttu-id="c498d-252">См. дополнительные сведения о [зонах и записях в Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="c498d-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="c498d-253">Узнайте, каким образом слишком[защиты зоны и записи](dns-protect-zones-recordsets.md) при использовании Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c498d-253">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="c498d-254">Просмотрите hello [справочная документация по Azure DNS PowerShell](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="c498d-254">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
